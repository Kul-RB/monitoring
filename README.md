# Задание
1. Используя директорию [help](./help) внутри этого домашнего задания, запустите связку prometheus-grafana.
2. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
3. Подключите поднятый вами prometheus, как источник данных.
4. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

# Решение
![image](https://github.com/Kul-RB/monitoring/assets/53901269/9d928d95-77c5-4d9e-9bae-0aea2959b990)

# Задание 
Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
1. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
1. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);
- CPULA 1/5/15;
- количество свободной оперативной памяти;
- количество места на файловой системе.

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

# Решение
1. 100 - (rate(node_cpu_seconds_total{mode="idle", instance="node1s.carfix.local:9100", cpu="0"}[5m]))
![image](https://github.com/Kul-RB/monitoring/assets/53901269/198ed4a4-682c-4d90-a010-922c4e700975)

2. node_load15{instance="node1s.carfix.local:9100",job="node1s"}
   node_load5{instance="node1s.carfix.local:9100",job="node1s"}
   node_load1{instance="node1s.carfix.local:9100",job="node1s"}
![image](https://github.com/Kul-RB/monitoring/assets/53901269/7469ecab-8c26-4e94-b144-6a28530ce8f3)

3. node_memory_MemFree_bytes{instance="node1s.carfix.local:9100", job="node1s"}
![image](https://github.com/Kul-RB/monitoring/assets/53901269/b21b511f-fcf5-4e08-ba33-3944f3353478)

4. node_filesystem_avail_bytes{instance="node1s.carfix.local:9100", job="node1s", mountpoint="/",fstype!="rootfs"}
![image](https://github.com/Kul-RB/monitoring/assets/53901269/3a449b75-d3c9-488f-a647-4637f39a5bd1)

# Задание 
1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
2. В качестве решения задания приведите скриншот вашей итоговой Dashboard.

# Решение
![image](https://github.com/Kul-RB/monitoring/assets/53901269/540e510a-a79e-4251-902a-65305a6c1964)

# Задание
1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
2. В качестве решения задания приведите листинг этого файла.

# Решение

```
{
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": {
          "type": "grafana",
          "uid": "-- Grafana --"
        },
        "enable": true,
        "hide": true,
        "iconColor": "rgba(0, 211, 255, 1)",
        "name": "Annotations & Alerts",
        "type": "dashboard"
      }
    ]
  },
  "editable": true,
  "fiscalYearStartMonth": 0,
  "graphTooltip": 0,
  "id": 6,
  "links": [],
  "liveNow": false,
  "panels": [
    {
      "datasource": {
        "type": "prometheus",
        "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "palette-classic"
          },
          "custom": {
            "axisBorderShow": false,
            "axisCenteredZero": false,
            "axisColorMode": "text",
            "axisLabel": "",
            "axisPlacement": "auto",
            "barAlignment": 0,
            "drawStyle": "line",
            "fillOpacity": 40,
            "gradientMode": "none",
            "hideFrom": {
              "legend": false,
              "tooltip": false,
              "viz": false
            },
            "insertNulls": false,
            "lineInterpolation": "linear",
            "lineWidth": 1,
            "pointSize": 5,
            "scaleDistribution": {
              "type": "linear"
            },
            "showPoints": "auto",
            "spanNulls": false,
            "stacking": {
              "group": "A",
              "mode": "percent"
            },
            "thresholdsStyle": {
              "mode": "off"
            }
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          }
        },
        "overrides": []
      },
      "gridPos": {
        "h": 8,
        "w": 12,
        "x": 0,
        "y": 0
      },
      "id": 1,
      "options": {
        "legend": {
          "calcs": [],
          "displayMode": "list",
          "placement": "bottom",
          "showLegend": true
        },
        "tooltip": {
          "mode": "single",
          "sort": "none"
        }
      },
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
          },
          "editorMode": "code",
          "expr": "100 - (rate(node_cpu_seconds_total{mode=\"idle\", instance=\"node1s.carfix.local:9100\", cpu=\"0\"}[5m]))",
          "instant": false,
          "legendFormat": "__auto",
          "range": true,
          "refId": "A"
        }
      ],
      "title": "CPU IDLE",
      "type": "timeseries"
    },
    {
      "datasource": {
        "type": "prometheus",
        "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "palette-classic"
          },
          "custom": {
            "axisBorderShow": false,
            "axisCenteredZero": false,
            "axisColorMode": "text",
            "axisLabel": "",
            "axisPlacement": "auto",
            "barAlignment": 0,
            "drawStyle": "line",
            "fillOpacity": 0,
            "gradientMode": "none",
            "hideFrom": {
              "legend": false,
              "tooltip": false,
              "viz": false
            },
            "insertNulls": false,
            "lineInterpolation": "linear",
            "lineWidth": 1,
            "pointSize": 5,
            "scaleDistribution": {
              "type": "linear"
            },
            "showPoints": "auto",
            "spanNulls": false,
            "stacking": {
              "group": "A",
              "mode": "none"
            },
            "thresholdsStyle": {
              "mode": "off"
            }
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "bytes"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 8,
        "w": 12,
        "x": 12,
        "y": 0
      },
      "id": 3,
      "options": {
        "legend": {
          "calcs": [],
          "displayMode": "list",
          "placement": "bottom",
          "showLegend": true
        },
        "tooltip": {
          "mode": "single",
          "sort": "none"
        }
      },
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
          },
          "editorMode": "code",
          "expr": "node_memory_MemFree_bytes{instance=\"node1s.carfix.local:9100\", job=\"node1s\"}",
          "instant": false,
          "legendFormat": "__auto",
          "range": true,
          "refId": "A"
        }
      ],
      "title": "RAM Free",
      "type": "timeseries"
    },
    {
      "datasource": {
        "type": "prometheus",
        "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "palette-classic"
          },
          "custom": {
            "axisBorderShow": false,
            "axisCenteredZero": false,
            "axisColorMode": "text",
            "axisLabel": "",
            "axisPlacement": "auto",
            "barAlignment": 0,
            "drawStyle": "line",
            "fillOpacity": 0,
            "gradientMode": "none",
            "hideFrom": {
              "legend": false,
              "tooltip": false,
              "viz": false
            },
            "insertNulls": false,
            "lineInterpolation": "linear",
            "lineWidth": 1,
            "pointSize": 5,
            "scaleDistribution": {
              "type": "linear"
            },
            "showPoints": "auto",
            "spanNulls": false,
            "stacking": {
              "group": "A",
              "mode": "none"
            },
            "thresholdsStyle": {
              "mode": "off"
            }
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          }
        },
        "overrides": []
      },
      "gridPos": {
        "h": 8,
        "w": 12,
        "x": 0,
        "y": 8
      },
      "id": 2,
      "options": {
        "legend": {
          "calcs": [],
          "displayMode": "list",
          "placement": "bottom",
          "showLegend": true
        },
        "tooltip": {
          "mode": "single",
          "sort": "none"
        }
      },
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
          },
          "editorMode": "code",
          "expr": "node_load15{instance=\"node1s.carfix.local:9100\",job=\"node1s\"}",
          "instant": false,
          "legendFormat": "node_load15",
          "range": true,
          "refId": "A"
        },
        {
          "datasource": {
            "type": "prometheus",
            "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
          },
          "editorMode": "code",
          "expr": "node_load5{instance=\"node1s.carfix.local:9100\",job=\"node1s\"}",
          "hide": false,
          "instant": false,
          "legendFormat": "node_load5",
          "range": true,
          "refId": "B"
        },
        {
          "datasource": {
            "type": "prometheus",
            "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
          },
          "editorMode": "code",
          "expr": "node_load1{instance=\"node1s.carfix.local:9100\",job=\"node1s\"}",
          "hide": false,
          "instant": false,
          "legendFormat": "node_load1",
          "range": true,
          "refId": "C"
        }
      ],
      "title": "CPULA",
      "type": "timeseries"
    },
    {
      "datasource": {
        "type": "prometheus",
        "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              }
            ]
          },
          "unit": "bytes"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 8,
        "w": 12,
        "x": 12,
        "y": 8
      },
      "id": 4,
      "options": {
        "colorMode": "none",
        "graphMode": "none",
        "justifyMode": "center",
        "orientation": "auto",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "textMode": "auto",
        "wideLayout": true
      },
      "pluginVersion": "10.2.2",
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "aca3fd63-be0c-4155-a6ae-b1a3de7eecab"
          },
          "editorMode": "code",
          "expr": "node_filesystem_avail_bytes{instance=\"node1s.carfix.local:9100\", job=\"node1s\", mountpoint=\"/\",fstype!=\"rootfs\"}",
          "instant": false,
          "legendFormat": "__auto",
          "range": true,
          "refId": "A"
        }
      ],
      "title": "Free diskspace",
      "type": "stat"
    }
  ],
  "refresh": "",
  "schemaVersion": 38,
  "tags": [],
  "templating": {
    "list": []
  },
  "time": {
    "from": "now-6h",
    "to": "now"
  },
  "timepicker": {},
  "timezone": "",
  "title": "netology",
  "uid": "f8c5532c-1579-4a8a-87a3-0a6893131030",
  "version": 2,
  "weekStart": ""
}
```
