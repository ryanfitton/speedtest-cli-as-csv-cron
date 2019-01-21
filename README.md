# Speedtest CLI tests via CRON as .csv

* Author: `Ryan Fitton <ryan@ryanfitton.co.uk>`
* Version: `1.0.0`
* Date: `21/01/2019`


## Requirements

* Python (`python-pip`)
* speedtest-cli ([Repo](https://github.com/sivel/speedtest-cli))
* speedtest-csv ([Repo](https://github.com/HenrikBengtsson/speedtest-cli-extras))


## Installation
1. Switch to the `root` user:

```
sudo su
```


2. Install `speedtest-cli`, run each line separately:

```
sudo apt-get install python-pip
sudo pip install speedtest-cli
```


3. Download the `speedtest-csv` script.
<strong>Note:</strong> A copy of this script is already stored in this repo, you can use this or re-download and make the changes to the file mentioned in step 5.

```
sudo wget -O speedtest-csv https://raw.githubusercontent.com/HenrikBengtsson/speedtest-cli-extras/master/bin/speedtest-csv
```


4. Now give the file execute permissions:

```
sudo chmod +x speedtest-csv
```


5. You will need to edit a line in the file to so that it can be run from CRON:

```
sudo nano speedtest-csv
```

Find the line `cmd="speedtest-cli $opts` and add `/usr/local/bin/` before it so it reads:

```
cmd="/usr/local/bin/speedtest-cli $opts"
```

save the file and exit.


6. Next move `speedtest-csv` to `/usr/bin/`:

```
sudo mv speedtest-csv /usr/bin/
```


7. Generate the CSV header:

```
sudo speedtest-csv --header >> /cron/speedtest/speedtest.csv
```


8. Add to the CRON:

```
sudo crontab -e
```


9. Add the following line to the end of the file, this example is daily, ever four hours:

```
0 */4 * * * speedtest-csv >> /cron/speedtest/speedtest.csv
```

save the file and exit.
