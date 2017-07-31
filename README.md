
## populate prometheus TPR without RuleSelector & ServiceMonitor

Prometheus Operator (re-)generates the configuration for the Prometheus instances based on the ConfigMaps it is able to find with the specified label selector: 

```sh
prometheus: custom
```

Prometheus Operator writes the names of those ConfigMaps into the Secret used for configuring Prometheus:

```sh
configmaps.json: |+
    {
      "items": [
        {
          "key": "testing/rule01"
        }
      ]
    }
```

Prometheus Operator generates the followingPrometheus configuration based on the configmaps being found in the configmaps.json:

```sh
    {
        "rule_files":[
            "/etc/prometheus/rules/rules-0/*.rules"
        ]
    }
```

The sidecar config-reloader then retrieves the ConfigMaps specified in the configmaps.json file and writes them into the directories as stated in the generated configuration.




