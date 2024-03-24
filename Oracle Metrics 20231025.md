```
## All options defined here are available to all instances.
#
init_config:

    ## @param use_instant_client - boolean - optional - default: false
    ## Determines whether the Agent uses the Oracle Instant Client to connect instead of the Oracle native client. 
    ## This option cannot be used at the same time as `jdbc_driver_path`.
    #
    # use_instant_client: false

    ## @param global_custom_queries - list of mappings - optional
    ## See `custom_queries` defined below.
    ##
    ## Global custom queries can be applied to all instances using the
    ## `use_global_custom_queries` setting at the instance level.
    #
    # global_custom_queries:
    #   - query: <QUERY>
    #     columns: <COLUMNS>
    #     tags: <TAGS>

    ## @param service - string - optional
    ## Attach the tag `service:<SERVICE>` to every metric, event, and service check emitted by this integration.
    ##
    ## Additionally, this sets the default `service` for every log source.
    #
    # service: <SERVICE>
  global_custom_queries:
    - query: |
          SELECT df.tablespace_name,
                 round(df.bytes / (1024 * 1024),0),
                 round(SUM(fs.bytes) / (1024 * 1024),0),
                 Nvl(Round(SUM(fs.bytes) * 100 / df.bytes),1),
                 Round((df.bytes - SUM(fs.bytes)) * 100 / df.bytes)
            FROM dba_free_space fs,
                 (SELECT tablespace_name,SUM(bytes) bytes
                    FROM dba_data_files
                   GROUP BY tablespace_name) df
          WHERE fs.tablespace_name (+)  = df.tablespace_name
          GROUP BY df.tablespace_name,df.bytes
          UNION ALL
          SELECT df.tablespace_name tspace,
                 round(fs.bytes / (1024 * 1024),0),
                 round(SUM(df.bytes_free) / (1024 * 1024),0),
                 Nvl(Round((SUM(fs.bytes) - df.bytes_used) * 100 / fs.bytes), 1),
                 Round((SUM(fs.bytes) - df.bytes_free) * 100 / fs.bytes)
            FROM dba_temp_files fs,
                 (SELECT tablespace_name,bytes_free,bytes_used
                    FROM v$temp_space_header
                   GROUP BY tablespace_name,bytes_free,bytes_used) df
          WHERE fs.tablespace_name (+)  = df.tablespace_name
          GROUP BY df.tablespace_name,fs.bytes,df.bytes_free,df.bytes_used
          ORDER BY 5 DESC
      columns:
        - name: r_tablespace.name
          type: tag
        - name: r_tablespace.size_mb
          type: gauge
        - name: r_tablespace.free_mb
          type: gauge
        - {}
        - name: r_tablespace.used_percentage
          type: gauge
      tags:
        - environment:staging
        - project:bpc_oracle
## Every instance is scheduled independently of the others.
#
instances:
  - server: localhost:1521
    service_name: svfe
    username: datadog
    password: a84dfd50a
    service: svfe
  - server: localhost:1521
    service_name: svfe
    username: cop_apps
    password: cop_apps1
    service: svfe
    use_global_custom_queries: extend
    custom_queries:
      - query: | 
          SELECT
            COUNT(*) AS smsgate_error_count
          FROM
            SMSGATE.T_UFD_MESSAGE_LOG T1
          JOIN
            SMSGATE.T_UFD_MESSAGE_STATUS_LOG T2
          ON
            T1.ID = T2.MESSAGE_ID
          WHERE
            T2.STATUS = 'ERROR' and T2.STATUS_TIME > CAST(SYSTIMESTAMP AS TIMESTAMP) - interval '5' minute
        columns:
          - name: smsgate.error_count
            type: gauge
        tags:
          - environment:staging
          - project:bpc_oracle
  - server: localhost:1521
    service_name: svbo
    username: MAIN
    password: MAIN1
    service: svbo
    use_global_custom_queries: extend
    custom_queries:
      - query: |
          select
            count(*) as svbo_container_error_count
          from prc_session ps
            join prc_process pp on pp.id = ps.process_id
          where ps.part_key between trunc(sysdate - 1) and trunc(sysdate + 1) - interval '1' second
          and ps.result_code in ('PRSR0003','PRSR0004')
          and ps.start_time > CAST(SYSTIMESTAMP AS TIMESTAMP) - interval '5' minute
        columns:
          - name: svbo.container_error_count
            type: gauge
        tags:
          - environment:staging
          - project:bpc_oracle
  - server: localhost:1521
    service_name: svacs
    username: ACS
    password: ACS1
    service: svacs
    use_global_custom_queries: extend
    custom_queries:
      - query: |
          SELECT count(*) as
            failed_transaction_count
          FROM CRES
            where TRANS_STATUS IN ('U', 'N','R') AND DATE_CREATED > CAST(SYSTIMESTAMP AS TIMESTAMP) - INTERVAL '5' MINUTE
        columns:
          - name: acs.failed_transaction_count
            type: gauge
        tags:
          - environment:staging
          - project:bpc_oracle
          - transaction:cres
      - query: |
          SELECT count(*) as
            failed_transaction_count
          FROM ARES
            where TRANS_STATUS IN ('U', 'N','R') AND DATE_CREATED > CAST(SYSTIMESTAMP AS TIMESTAMP) - INTERVAL '5' MINUTE
        columns:
          - name: acs.failed_transaction_count
            type: gauge
        tags:
          - environment:staging
          - project:bpc_oracle
          - transaction:ares
  - server: localhost:1521
    service_name: svcg
    username: SVCG
    password: SVCG1
    service: svcg
    use_global_custom_queries: extend
    custom_queries:
      - query: |
          select
           count(*) as svcg_process_error_count
           from mtr_process pp
           join mtr_card_process pc on pc.process_id = pp.id
           left join mtr_card_process_error ce on ce.card_process_id = pc.id
           where pp.start_date > ((SYSDATE - TO_DATE('1970-01-01', 'yyyy-mm-dd')) * 24 * 60 * 60 * 1000) - 300000
        columns:
          - name: svcg.process_error_count
            type: gauge
        tags:
          - environment:staging
          - project:bpc_oracle
```