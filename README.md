# Forest Fire

Read metrics from a serial port device (eg. Arduino) and export to [Prometheus](https://prometheus.io).

Expects data on the serial port in a simple format:

```
metric1:sensor1:1.44, metric1:sensor2:2.71, metric2:sensor3:3.14
```

All metrics have type `gauge` with noly one label `sensor`.

## Installation

```
cd ~
sudo apt-get install python3 virtualenv git
git clone https://github.com/vickenty/forest_fire
cd forest_fire
virtualenv -p python3 venv
venv/bin/pip install -r requirements.txt
```

## Running on startup

```
cd ~/forest_fire
cp forest_fire.service /etc/systemd/system
systemctl daemon-reload
systemctl enable forest_fire
systemctl start forest_fire
```

## Example prometheus.yml

```
global:
  scrape_interval: 10s
scrape_configs:
- job_name: forest_fire
  static_configs:
  - targets: [ "localhost:8081" ]
```
