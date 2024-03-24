so to run datadog agent on top of VM you'll need to run this 
```
DD_API_KEY=${dd_api_key} DD_SITE="datadoghq.com" DD_APM_INSTRUMENTATION_ENABLED=host bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_script_agent7.sh)"
```

the script will install datadog agent, this is the behavior from inside of the VM:
- it will create systemctl entry called `datadog-agent`
- there is a command called `datadog-agent status` to check the status of the VM

as for on the dashboard side, infrastructure list unable to give you the correct entry from IP, you'll need to give EC2 instance ID