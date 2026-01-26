To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo hostnamectl set-hostname spacedeck
[sudo] password for spacedeck: 
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ wget -q -O - https://apt.grafana.com/gpg.key | sudo apt-key add -
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
OK
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo apt update
Hit:1 http://my.archive.ubuntu.com/ubuntu noble InRelease
Hit:2 http://my.archive.ubuntu.com/ubuntu noble-updates InRelease
Hit:3 http://my.archive.ubuntu.com/ubuntu noble-backports InRelease
Hit:4 http://security.ubuntu.com/ubuntu noble-security InRelease
Reading package lists... Done         
Building dependency tree... Done
Reading state information... Done
79 packages can be upgraded. Run 'apt list --upgradable' to see them.
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo apt install grafana=11.2.0 -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package grafana
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo apt install -y gnupg2 curl
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  curl gnupg2
0 upgraded, 2 newly installed, 0 to remove and 79 not upgraded.
Need to get 231 kB of archives.
After this operation, 566 kB of additional disk space will be used.
Get:1 http://my.archive.ubuntu.com/ubuntu noble-updates/main amd64 curl amd64 8.5.0-2ubuntu10.6 [226 kB]
Get:2 http://security.ubuntu.com/ubuntu noble-security/universe amd64 gnupg2 all 2.4.4-2ubuntu17.4 [4,752 B]
Fetched 231 kB in 2s (138 kB/s)    
Selecting previously unselected package curl.
(Reading database ... 150423 files and directories currently installed.)
Preparing to unpack .../curl_8.5.0-2ubuntu10.6_amd64.deb ...
Unpacking curl (8.5.0-2ubuntu10.6) ...
Selecting previously unselected package gnupg2.
Preparing to unpack .../gnupg2_2.4.4-2ubuntu17.4_all.deb ...
Unpacking gnupg2 (2.4.4-2ubuntu17.4) ...
Setting up gnupg2 (2.4.4-2ubuntu17.4) ...
Setting up curl (8.5.0-2ubuntu10.6) ...
Processing triggers for man-db (2.12.0-4build2) ...
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo mkdir -p /etc/apt/keyrings/
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo apt update
Hit:1 http://my.archive.ubuntu.com/ubuntu noble InRelease
Hit:2 http://my.archive.ubuntu.com/ubuntu noble-updates InRelease                                
Hit:3 http://my.archive.ubuntu.com/ubuntu noble-backports InRelease                              
Get:4 https://apt.grafana.com stable InRelease [7,661 B]                                         
Hit:5 http://security.ubuntu.com/ubuntu noble-security InRelease           
Get:6 https://apt.grafana.com stable/main amd64 Packages [456 kB]
Fetched 464 kB in 2s (261 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
79 packages can be upgraded. Run 'apt list --upgradable' to see them.
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo apt install grafana=11.2.0 -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  musl
The following NEW packages will be installed:
  grafana musl
0 upgraded, 2 newly installed, 0 to remove and 79 not upgraded.
Need to get 123 MB of archives.
After this operation, 464 MB of additional disk space will be used.
Get:1 http://my.archive.ubuntu.com/ubuntu noble/universe amd64 musl amd64 1.2.4-2 [416 kB]
Get:2 https://apt.grafana.com stable/main amd64 grafana amd64 11.2.0 [123 MB]                        
Fetched 123 MB in 13s (9,124 kB/s)                                                                   
Selecting previously unselected package musl:amd64.
(Reading database ... 150436 files and directories currently installed.)
Preparing to unpack .../musl_1.2.4-2_amd64.deb ...
Unpacking musl:amd64 (1.2.4-2) ...
Selecting previously unselected package grafana.
Preparing to unpack .../grafana_11.2.0_amd64.deb ...
Unpacking grafana (11.2.0) ...
Setting up musl:amd64 (1.2.4-2) ...
Setting up grafana (11.2.0) ...
info: Selecting UID from range 100 to 999 ...

info: Adding system user `grafana' (UID 122) ...
info: Adding new user `grafana' (UID 122) with group `grafana' ...
info: Not creating home directory `/usr/share/grafana'.
### NOT starting on installation, please execute the following statements to configure grafana to star
t automatically using systemd
 sudo /bin/systemctl daemon-reload
 sudo /bin/systemctl enable grafana-server
### You can start grafana-server by executing
 sudo /bin/systemctl start grafana-server
Processing triggers for man-db (2.12.0-4build2) ...
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo systemctl enable grafana-server
Synchronizing state of grafana-server.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable grafana-server
Created symlink /etc/systemd/system/multi-user.target.wants/grafana-server.service → /usr/lib/systemd/system/grafana-server.service.
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo systemctl start grafana-server
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo nano /etc/grafana/grafana.ini
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo nano /etc/grafana/grafana.ini
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo grafana-cli admin reset-admin-password admin
INFO [01-26|17:11:36] Starting Grafana                         logger=settings version= commit= branch= compiled=1970-01-01T07:30:00+07:30
INFO [01-26|17:11:36] Config loaded from                       logger=settings file=/usr/share/grafana/conf/defaults.ini
INFO [01-26|17:11:36] Config loaded from                       logger=settings file=/etc/grafana/grafana.ini
INFO [01-26|17:11:36] Config overridden from command line      logger=settings arg="default.paths.data=/var/lib/grafana"
INFO [01-26|17:11:36] Config overridden from command line      logger=settings arg="default.paths.logs=/var/log/grafana"
INFO [01-26|17:11:36] Config overridden from command line      logger=settings arg="default.paths.plugins=/var/lib/grafana/plugins"
INFO [01-26|17:11:36] Config overridden from command line      logger=settings arg="default.paths.provisioning=/etc/grafana/provisioning"
INFO [01-26|17:11:36] Target                                   logger=settings target=[all]
INFO [01-26|17:11:36] Path Home                                logger=settings path=/usr/share/grafana
INFO [01-26|17:11:36] Path Data                                logger=settings path=/var/lib/grafana
INFO [01-26|17:11:36] Path Logs                                logger=settings path=/var/log/grafana
INFO [01-26|17:11:36] Path Plugins                             logger=settings path=/var/lib/grafana/plugins
INFO [01-26|17:11:36] Path Provisioning                        logger=settings path=/etc/grafana/provisioning
INFO [01-26|17:11:36] App mode production                      logger=settings
INFO [01-26|17:11:36] FeatureToggles                           logger=featuremgmt correlations=true managedPluginsInstall=true prometheusAzureOverrideAudience=true tlsMemcached=true awsAsyncQueryCaching=true alertingInsights=true prometheusConfigOverhaulAuth=true cloudWatchRoundUpEndTime=true prometheusDataplane=true logRowsPopoverMenu=true prometheusMetricEncyclopedia=true cloudWatchNewLabelParsing=true recordedQueriesMulti=true autoMigrateXYChartPanel=true kubernetesPlaylists=true lokiQueryHints=true addFieldFromCalculationStatFunctions=true publicDashboards=true panelMonitoring=true alertingSimplifiedRouting=true dashgpt=true recoveryThreshold=true ssoSettingsApi=true dataplaneFrontendFallback=true angularDeprecationUI=true transformationsVariableSupport=true groupToNestedTableTransformation=true exploreMetrics=true formatString=true lokiStructuredMetadata=true logsInfiniteScrolling=true cloudWatchCrossAccountQuerying=true lokiMetricDataplane=true influxdbBackendMigration=true logsExploreTableVisualisation=true lokiQuerySplitting=true topnav=true logsContextDatasourceUi=true transformationsRedesign=true alertingNoDataErrorExecution=true nestedFolders=true annotationPermissionUpdate=true
INFO [01-26|17:11:36] Connecting to DB                         logger=sqlstore dbtype=sqlite3
INFO [01-26|17:11:36] Locking database                         logger=migrator
INFO [01-26|17:11:36] Starting DB migrations                   logger=migrator
INFO [01-26|17:11:36] migrations completed                     logger=migrator performed=0 skipped=594 duration=346.646µs
INFO [01-26|17:11:36] Unlocking database                       logger=migrator
INFO [01-26|17:11:36] Envelope encryption state                logger=secrets enabled=true current provider=secretKey.v1

Admin password changed successfully ✔

spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo systemctl restart grafana-server
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo apt install postgresql postgresql-contrib -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libcommon-sense-perl libjson-perl libjson-xs-perl libllvm17t64 libpq5 libtypes-serialiser-perl postgresql-16
  postgresql-client-16 postgresql-client-common postgresql-common
Suggested packages:
  postgresql-doc postgresql-doc-16
The following NEW packages will be installed:
  libcommon-sense-perl libjson-perl libjson-xs-perl libllvm17t64 libpq5 libtypes-serialiser-perl postgresql
  postgresql-16 postgresql-client-16 postgresql-client-common postgresql-common postgresql-contrib
0 upgraded, 12 newly installed, 0 to remove and 80 not upgraded.
Need to get 43.6 MB of archives.
After this operation, 175 MB of additional disk space will be used.
Get:1 http://my.archive.ubuntu.com/ubuntu noble/main amd64 libjson-perl all 4.10000-1 [81.9 kB]
Get:2 http://my.archive.ubuntu.com/ubuntu noble-updates/main amd64 postgresql-client-common all 257build1.1 [36.4 kB]
Get:3 http://my.archive.ubuntu.com/ubuntu noble-updates/main amd64 postgresql-common all 257build1.1 [161 kB]
Get:4 http://my.archive.ubuntu.com/ubuntu noble/main amd64 libcommon-sense-perl amd64 3.75-3build3 [20.4 kB]
Get:5 http://my.archive.ubuntu.com/ubuntu noble/main amd64 libtypes-serialiser-perl all 1.01-1 [11.6 kB]
Get:6 http://my.archive.ubuntu.com/ubuntu noble-updates/main amd64 libjson-xs-perl amd64 4.040-0ubuntu0.24.04.1 [83.7 kB]
Get:7 http://my.archive.ubuntu.com/ubuntu noble/main amd64 libllvm17t64 amd64 1:17.0.6-9ubuntu1 [26.2 MB]
Get:8 http://security.ubuntu.com/ubuntu noble-security/main amd64 libpq5 amd64 16.11-0ubuntu0.24.04.1 [145 kB]
Get:9 http://my.archive.ubuntu.com/ubuntu noble-updates/main amd64 postgresql all 16+257build1.1 [11.6 kB]
Get:10 http://my.archive.ubuntu.com/ubuntu noble-updates/main amd64 postgresql-contrib all 16+257build1.1 [11.6 kB]
Get:11 http://security.ubuntu.com/ubuntu noble-security/main amd64 postgresql-client-16 amd64 16.11-0ubuntu0.24.04.1 [1,297 kB]
Get:12 http://security.ubuntu.com/ubuntu noble-security/main amd64 postgresql-16 amd64 16.11-0ubuntu0.24.04.1 [15.6 MB]
Fetched 43.6 MB in 6s (7,264 kB/s)         
Preconfiguring packages ...
Selecting previously unselected package libjson-perl.
(Reading database ... 160163 files and directories currently installed.)
Preparing to unpack .../00-libjson-perl_4.10000-1_all.deb ...
Unpacking libjson-perl (4.10000-1) ...
Selecting previously unselected package postgresql-client-common.
Preparing to unpack .../01-postgresql-client-common_257build1.1_all.deb ...
Unpacking postgresql-client-common (257build1.1) ...
Selecting previously unselected package postgresql-common.
Preparing to unpack .../02-postgresql-common_257build1.1_all.deb ...
Adding 'diversion of /usr/bin/pg_config to /usr/bin/pg_config.libpq-dev by postgresql-common'
Unpacking postgresql-common (257build1.1) ...
Selecting previously unselected package libcommon-sense-perl:amd64.
Preparing to unpack .../03-libcommon-sense-perl_3.75-3build3_amd64.deb ...
Unpacking libcommon-sense-perl:amd64 (3.75-3build3) ...
Selecting previously unselected package libtypes-serialiser-perl.
Preparing to unpack .../04-libtypes-serialiser-perl_1.01-1_all.deb ...
Unpacking libtypes-serialiser-perl (1.01-1) ...
Selecting previously unselected package libjson-xs-perl.
Preparing to unpack .../05-libjson-xs-perl_4.040-0ubuntu0.24.04.1_amd64.deb ...
Unpacking libjson-xs-perl (4.040-0ubuntu0.24.04.1) ...
Selecting previously unselected package libllvm17t64:amd64.
Preparing to unpack .../06-libllvm17t64_1%3a17.0.6-9ubuntu1_amd64.deb ...
Unpacking libllvm17t64:amd64 (1:17.0.6-9ubuntu1) ...
Selecting previously unselected package libpq5:amd64.
Preparing to unpack .../07-libpq5_16.11-0ubuntu0.24.04.1_amd64.deb ...
Unpacking libpq5:amd64 (16.11-0ubuntu0.24.04.1) ...
Selecting previously unselected package postgresql-client-16.
Preparing to unpack .../08-postgresql-client-16_16.11-0ubuntu0.24.04.1_amd64.deb ...
Unpacking postgresql-client-16 (16.11-0ubuntu0.24.04.1) ...
Selecting previously unselected package postgresql-16.
Preparing to unpack .../09-postgresql-16_16.11-0ubuntu0.24.04.1_amd64.deb ...
Unpacking postgresql-16 (16.11-0ubuntu0.24.04.1) ...
Selecting previously unselected package postgresql.
Preparing to unpack .../10-postgresql_16+257build1.1_all.deb ...
Unpacking postgresql (16+257build1.1) ...
Selecting previously unselected package postgresql-contrib.
Preparing to unpack .../11-postgresql-contrib_16+257build1.1_all.deb ...
Unpacking postgresql-contrib (16+257build1.1) ...
Setting up postgresql-client-common (257build1.1) ...
Setting up libpq5:amd64 (16.11-0ubuntu0.24.04.1) ...
Setting up libcommon-sense-perl:amd64 (3.75-3build3) ...
Setting up libllvm17t64:amd64 (1:17.0.6-9ubuntu1) ...
Setting up libtypes-serialiser-perl (1.01-1) ...
Setting up libjson-perl (4.10000-1) ...
Setting up libjson-xs-perl (4.040-0ubuntu0.24.04.1) ...
Setting up postgresql-client-16 (16.11-0ubuntu0.24.04.1) ...
update-alternatives: using /usr/share/postgresql/16/man/man1/psql.1.gz to provide /usr/share/man/man1/psql.1.gz (psql.1.
gz) in auto mode
Setting up postgresql-common (257build1.1) ...

Creating config file /etc/postgresql-common/createcluster.conf with new version
Building PostgreSQL dictionaries from installed myspell/hunspell packages...
  en_us
Removing obsolete dictionary files:
Created symlink /etc/systemd/system/multi-user.target.wants/postgresql.service → /usr/lib/systemd/system/postgresql.serv
ice.
Setting up postgresql-16 (16.11-0ubuntu0.24.04.1) ...
Creating new PostgreSQL cluster 16/main ...
/usr/lib/postgresql/16/bin/initdb -D /var/lib/postgresql/16/main --auth-local peer --auth-host scram-sha-256 --no-instru
ctions
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "en_US.UTF-8".
The default database encoding has accordingly been set to "UTF8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

fixing permissions on existing directory /var/lib/postgresql/16/main ... ok
creating subdirectories ... ok
selecting dynamic shared memory implementation ... posix
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting default time zone ... Asia/Kuala_Lumpur
creating configuration files ... ok
running bootstrap script ... ok
performing post-bootstrap initialization ... ok
syncing data to disk ... ok
Setting up postgresql-contrib (16+257build1.1) ...
Setting up postgresql (16+257build1.1) ...
Processing triggers for man-db (2.12.0-4build2) ...
Processing triggers for libc-bin (2.39-0ubuntu8.6) ...
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo -u postgres psql -c "CREATE DATABASE satellite_db;"
CREATE DATABASE
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo -u postgres psql -c "CREATE USER astro WITH PASSWORD 'AstroPass2024!';"
bash: !': event not found
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo -u postgres psql -c "CREATE USER astro WITH PASSWORD 'AstroPass2024\!'; "
CREATE ROLE
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE satellite_db TO astro;"
GRANT
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo useradd -m -s /bin/bash astro
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ echo "astro:AstroPass2024\!" | sudo chpasswd
BAD PASSWORD: The password contains the user name in some form
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo -u astro mkdir -p /home/astro/{.ssh,.config}
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo apt install nginx -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  nginx-common
Suggested packages:
  fcgiwrap nginx-doc
The following NEW packages will be installed:
  nginx nginx-common
0 upgraded, 2 newly installed, 0 to remove and 80 not upgraded.
Need to get 564 kB of archives.
After this operation, 1,596 kB of additional disk space will be used.
Get:1 http://my.archive.ubuntu.com/ubuntu noble-updates/main amd64 nginx-common all 1.24.0-2ubuntu7.5 [43.4 kB]
Get:2 http://my.archive.ubuntu.com/ubuntu noble-updates/main amd64 nginx amd64 1.24.0-2ubuntu7.5 [520 kB]
Fetched 564 kB in 0s (1,653 kB/s)
Preconfiguring packages ...
Selecting previously unselected package nginx-common.
(Reading database ... 162122 files and directories currently installed.)
Preparing to unpack .../nginx-common_1.24.0-2ubuntu7.5_all.deb ...
Unpacking nginx-common (1.24.0-2ubuntu7.5) ...
Selecting previously unselected package nginx.
Preparing to unpack .../nginx_1.24.0-2ubuntu7.5_amd64.deb ...
Unpacking nginx (1.24.0-2ubuntu7.5) ...
Setting up nginx-common (1.24.0-2ubuntu7.5) ...
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /usr/lib/systemd/system/nginx.service.
Setting up nginx (1.24.0-2ubuntu7.5) ...
 * Upgrading binary nginx                                                                                        [ OK ] 
Processing triggers for man-db (2.12.0-4build2) ...
Processing triggers for ufw (0.36.2-6) ...
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo mkdir -p /var/www/spacedeck
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo chown -R www-data:www-data /var/www/spacedeck
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ sudo cp /tmp/SpaceDeck_WebFiles/* /var/www/spacedeck/
cp: cannot stat '/tmp/SpaceDeck_WebFiles/*': No such file or directory
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ ls -F
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ ls -F
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ ls -F ~
Desktop/  Documents/  Downloads/  Music/  Pictures/  Public/  snap/  Templates/  Videos/
spacedeck@spacedeck-VMware-Virtual-Platform:~/Desktop$ 

