namebench assesses a list of DNS servers you provide in order to determine which provide the fastest responses. namebench runs a fair and thorough benchmark using datasets in order to provide an individualized recommendation. This project began as a 20% project at Google **but has been modified to assess name servers of a specified host verse finding optimal name servers for general DNS resolution.**

namebench runs on Mac OS X, Windows, and UNIX, and is available with a graphical user interface as well as a command-line interface. **GUI not supported with this version at the moment.**

Requirements:

  * You have added your domains records to the name server to use, e.g. `dig www.domain.com @nameserverIP` will resolve.
  * Python 2.4 - 2.7. If you are using Mac OS X or Linux, this is built-in. Otherwise, visit http://www.python.org/ **Only tested using Python 2.7.x on Debian Linux and OS X.**

## Quick Use Guide

Edit `data/domain-list.txt` and the `[global]` section of `config/server_sources.cfg` with the name servers you want to benchmark. Then run:

 `sudo ./namebench.py -i data/domain-list.txt -z config/server_sources.cfg -x`

namebench comes with two interfaces: a simple graphical interface, and a more advanced command-line interface. If you have downloaded the versions for Mac OS X and Windows, you will get the graphical interface by default. **GUI not supported with this version at the moment.**

## Credit

namebench includes some wonderful third party software:

 * dnspython 1.12.0 (http://www.dnspython.org/)
 * httplib2 0.6.0 (http://code.google.com/p/httplib2/)
 * graphy 1.0 (http://graphy.googlecode.com/)
 * jinja2 2.2.1 (http://jinja.pocoo.org/2/)
 * python 2.5 pkg_resources (http://www.python.org/) 
 * simplejson 2.1.1 (http://code.google.com/p/simplejson/)
 * Crystal SVG icons (http://www.everaldo.com/crystal/)

For licensing information, see the LICENSE file within the appropriate subdirectory.

## Options
```
Usage: namebench.py [options]

Options:
  -h, --help            show this help message and exit
  -r RUN_COUNT, --runs=RUN_COUNT
                        Number of test runs to perform on each nameserver.
  -z CONFIG, --config=CONFIG
                        Config file to use.
  -o OUTPUT_FILE, --output=OUTPUT_FILE
                        Filename to write output to
  -t TEMPLATE, --template=TEMPLATE
                        Template to use for output generation (ascii, html,
                        resolv.conf)
  -c CSV_FILE, --csv_output=CSV_FILE
                        Filename to write query details to (CSV)
  -j HEALTH_THREAD_COUNT, --health_threads=HEALTH_THREAD_COUNT
                        # of health check threads to use
  -J BENCHMARK_THREAD_COUNT, --benchmark_threads=BENCHMARK_THREAD_COUNT
                        # of benchmark threads to use
  -P PING_TIMEOUT, --ping_timeout=PING_TIMEOUT
                        # of seconds ping requests timeout in.
  -y TIMEOUT, --timeout=TIMEOUT
                        # of seconds general requests timeout in.
  -Y HEALTH_TIMEOUT, --health_timeout=HEALTH_TIMEOUT
                        health check timeout (in seconds)
  -i INPUT_SOURCE, --input=INPUT_SOURCE
                        Import hostnames from an filename or application
                        (alexa, cachehit, cachemiss, cachemix, camino, chrome,
                        chromium, epiphany, firefox, flock, galeon, icab,
                        internet_explorer, konqueror, midori, omniweb, opera,
                        safari, seamonkey, squid, sunrise)
  -I, --invalidate_cache
                        Force health cache to be invalidated
  -q QUERY_COUNT, --query_count=QUERY_COUNT
                        Number of queries per run.
  -m SELECT_MODE, --select_mode=SELECT_MODE
                        Selection algorithm to use (weighted, random, chunk)
  -s NUM_SERVERS, --num_servers=NUM_SERVERS
                        Number of nameservers to include in test
  -S, --system_only     Only test the currently configured system
  - nameservers.
  -w, --open_webbrowser
                        Opens the final report in your browser
  -u, --upload_results  Upload anonmyized results to SITE_URLl (default:
                        False)
  -U SITE_URL, --site_url=SITE_URL
                        URL to upload results to
                        (http://namebench.appspot.com/)
  -H, --hide_results    Upload results, but keep them hidden from indexes.
  -x, --no_gui          Disable GUI
  -C, --enable-censorship-checks
                        Enable censorship checks
  -6, --ipv6_only       Only include IPv6 name servers
  -O, --only            Only test nameservers passed as arguments
```

## Sample Output
```
namebench 1.3.1 - data/shortlist.txt (automatic) on 2015-07-17 18:50:02.760017
threads=40/2 queries=250 runs=1 timeout=3.5 health_timeout=3.75 servers=5
------------------------------------------------------------------------------
- Reading data/shortlist.txt: data/shortlist.txt (0.0MB)
- Generating tests from data/shortlist.txt (1 records, selecting 250 automatic)
- Selecting 250 out of 1 sanitized records (weighted mode).

Odd - no built-in nameservers found.
- Checking query interception status...
- Checking connection quality: 1/3...3/3
- Congestion level is 0.09X (check duration: 3.66ms)
- Checking latest sanity reference
- Checking nameserver availability (23 threads): 0/23............23/23
- 23 of 23 servers are available (duration: 0:00:00.530555)
- Removing secondary nameservers slower than 16.85ms (max=400)
- Running initial health checks on 23 servers (23 threads): 0/23............23/23
- 23 of 23 tested name servers are healthy
- Waiting for wildcard cache queries from 23 servers (23 threads): 0/23............23/23
- Waiting 4s for TTL's to decrement.
- Running cache-sharing checks on 23 servers (40 threads): 0/506...........................................................................................................................................................................342..................................................................................505x.506/506
- Running final health checks on 23 servers (23 threads): 0/23............23/23

Final list of nameservers considered:
------------------------------------------------------------------------------
2001:470:200::2 HE 2 IPv6          4   ms | Responded with: NOERROR
216.218.131.2   HE 2               5   ms | Responded with: NOERROR
2001:470:300::2 HE 3 IPv6          5   ms | Responded with: NOERROR
216.66.80.18    HE 5               5   ms | Responded with: NOERROR
2400:cb00:2049: CF Ram IPv6        5   ms | Responded with: NXDOMAIN, Responded with: REFUSED
216.218.130.2   HE 1               5   ms | Responded with: NOERROR
216.66.1.2      HE 4               6   ms | Responded with: NOERROR
2001:470:500::2 HE 5 IPv6          6   ms | Responded with: NOERROR
173.245.59.225  CF Ram             6   ms | Responded with: NXDOMAIN, Responded with: REFUSED
216.218.132.2   HE 3               6   ms | Responded with: NOERROR
2600:3c03::a    Linode 4 IPv6      6   ms | Responded with: REFUSED
2001:470:400::2 HE 4 IPv6          6   ms | Responded with: NOERROR
173.245.58.113  CF Erin            6   ms | Responded with: NXDOMAIN, Responded with: REFUSED
207.192.70.10   Linode 4           7   ms | Responded with: REFUSED
2400:cb00:2049: CF Erin IPv6       9   ms | Responded with: NXDOMAIN, Responded with: REFUSED
75.127.96.10    Linode 3           18  ms | Responded with: REFUSED
2600:3c02::a    Linode 3 IPv6      19  ms | Responded with: REFUSED
2600:3c00::a    Linode 1 IPv6      38  ms | Responded with: REFUSED
69.93.127.10    Linode 1           39  ms | Responded with: REFUSED
2a01:7e00::a    Linode 5 IPv6      60  ms | Responded with: REFUSED
65.19.178.10    Linode 2           62  ms | Responded with: REFUSED
2600:3c01::a    Linode 2 IPv6      62  ms | Responded with: REFUSED
109.74.194.10   Linode 5           66  ms | Responded with: REFUSED

- Sending 250 queries to 23 servers: 0/5750..............................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................1173.......................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................2327....................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................3497...........................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................4691.........................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................5750/5750
- Error querying Linode 3 IPv6 [2600:3c02::a]: www.rsreese.com.: Timeout
- Error querying HE 2 [216.218.131.2]: www.rsreese.com.: Timeout
- Error querying Linode 4 [207.192.70.10]: www.rsreese.com.: Timeout
- Error querying Linode 4 IPv6 [2600:3c03::a]: www.rsreese.com.: Timeout
- Error querying Linode 4 [207.192.70.10]: www.rsreese.com.: Timeout
- Error querying Linode 4 IPv6 [2600:3c03::a]: www.rsreese.com.: Timeout
- Error querying Linode 4 [207.192.70.10]: www.rsreese.com.: Timeout
- Error querying Linode 3 IPv6 [2600:3c02::a]: www.rsreese.com.: Timeout

Fastest individual response (in milliseconds):
----------------------------------------------
HE 4             ## 1.51706
HE 2             ## 1.54209
HE 5             ## 1.55783
HE 5 IPv6        ## 1.56593
HE 3             ## 1.57809
HE 3 IPv6        ## 1.58215
HE 2 IPv6        ## 1.59001
HE 4 IPv6        ## 1.62697
HE 1             ## 1.64413
CF Erin          ## 2.01702
CF Ram           ## 2.03323
CF Ram IPv6      ## 2.07806
CF Erin IPv6     ## 2.16198
Linode 4         ### 3.99184
Linode 4 IPv6    #### 4.15397
Linode 3         ############### 20.12897
Linode 3 IPv6    ################ 20.98393
Linode 1 IPv6    ################################ 42.27901
Linode 1         ################################# 43.82300
Linode 5 IPv6    #################################################### 69.56506
Linode 2 IPv6    #################################################### 69.89813
Linode 5         ##################################################### 70.48488
Linode 2         ##################################################### 71.46811

Mean response (in milliseconds):
--------------------------------
HE 4             ## 2.42
HE 3             ## 2.50
HE 5             ## 2.50
HE 2 IPv6        ## 2.56
HE 3 IPv6        ## 2.58
HE 4 IPv6        ## 2.62
HE 5 IPv6        ## 2.68
HE 1             ## 2.78
CF Ram           ### 3.80
CF Erin IPv6     ### 4.35
CF Ram IPv6      ### 4.50
CF Erin          #### 6.11
HE 2             ########### 16.42
Linode 3         ################## 26.99
Linode 4 IPv6    ####################### 35.70
Linode 1 IPv6    ############################### 47.72
Linode 1         ################################ 49.34
Linode 4         ################################ 49.83
Linode 3 IPv6    ############################################ 67.76
Linode 5 IPv6    ############################################### 73.06
Linode 2 IPv6    ################################################# 75.02
Linode 2         ################################################# 75.70
Linode 5         ##################################################### 82.70

Response Distribution Chart URL (200ms):
----------------------------------------
http://chart.apis.google.com/chart?cht=lxy&chs=720x415&chxt=x,y&chg=10,20&chxr=0,0,200|1,0,100&chd=t:0,1,2,2,3,131|0,0,86,93,97,100|0,1,2,2,4,82|0,1,82,93,98,100|0,1,2,3,4,54|0,0,84,94,98,100|0,1,2,2,4,55|0,0,82,91,97,100|0,1,2,3,8|0,0,92,97,100|0,1,1,1750|0,0,97,100|0,1,2,2|0,0,96,100|0,1,2,3,3|0,0,94,99,100|0,1,2,4|0,0,97,100|0,1,1,3|0,0,97,100|0,1,2,5|0,0,96,100|0,1,2,3,4|0,0,96,100,100|0,1,2,2,7|0,0,93,98,100|0,22,23,24,25,26,26,27,28,29|0,0,16,39,61,78,91,96,100,100|0,21,23,23,24,25,26,26,28,30|0,0,13,46,67,79,89,95,98,100|0,36,36,37,38,39,39,41,87|0,0,7,46,78,87,93,97,100|0,35,36,37,38,39,40,46|0,0,13,51,66,91,97,100|0,10,11,12,12,13,14,15,15,22,24,41|0,0,5,36,63,72,78,82,86,93,98,100|0,10,11,12,13,13,15,16,16,18,1750|0,0,5,36,58,75,81,86,94,98,100|0,2,3,3,4,5,6,6,9,1750|0,0,7,46,74,84,90,94,98,100|0,2,3,4,4,5,6,8,1750|0,0,8,56,74,87,94,98,100|0,35,37,37,38,39,40,40,42,43,44,45,46,48,50,75|0,0,4,14,30,41,50,55,59,64,74,83,90,93,97,100|0,35,35,36,37,38,39,40,44|0,0,7,46,83,92,96,100,100&chco=ff9900,1a00ff,ff00e6,80ff00,00e6ff,fae30a,BE81F7,9f5734,000000,ff0000,3090c0,477248f,ababab,7b9f34,00ff00,0000ff,9900ff,405090,051290,f3e000,9030f0,f03060,e0a030&chxt=x,y,x,y&chxl=2:||Duration+in+ms||3:||%25|&chdl=CF+Erin|CF+Erin+IPv6|CF+Ram|CF+Ram+IPv6|HE+1|HE+2|HE+2+IPv6|HE+3|HE+3+IPv6|HE+4|HE+4+IPv6|HE+5|HE+5+IPv6|Linode+1|Linode+1+IPv6|Linode+2|Linode+2+IPv6|Linode+3|Linode+3+IPv6|Linode+4|Linode+4+IPv6|Linode+5|Linode+5+IPv6

Response Distribution Chart URL (Full):
---------------------------------------
http://chart.apis.google.com/chart?cht=lxy&chs=720x415&chxt=x,y&chg=10,20&chxr=0,0,3500|1,0,100&chd=t:0,0,0,0,0,8|0,0,86,93,97,100|0,0,0,0,0,5|0,1,82,93,98,100|0,0,0,0,0,3|0,0,84,94,98,100|0,0,0,0,0,3|0,0,82,91,97,100|0,0,0,0,0|0,0,92,97,100|0,0,0,100|0,0,97,100|0,0,0,0|0,0,96,100|0,0,0,0,0|0,0,94,99,100|0,0,0,0|0,0,97,100|0,0,0,0|0,0,97,100|0,0,0,0|0,0,96,100|0,0,0,0,0|0,0,96,100,100|0,0,0,0,0|0,0,93,98,100|0,1,1,1,1,1,2,2,2,2|0,0,16,39,61,78,91,96,100,100|0,1,1,1,1,1,1,1,2,2|0,0,13,46,67,79,89,95,98,100|0,2,2,2,2,2,2,2,5|0,0,7,46,78,87,93,97,100|0,2,2,2,2,2,2,3|0,0,13,51,66,91,97,100|0,1,1,1,1,1,1,1,1,1,1,2|0,0,5,36,63,72,78,82,86,93,98,100|0,1,1,1,1,1,1,1,1,1,100|0,0,5,36,58,75,81,86,94,98,100|0,0,0,0,0,0,0,0,0,100|0,0,7,46,74,84,90,94,98,100|0,0,0,0,0,0,0,0,100|0,0,8,56,74,87,94,98,100|0,2,2,2,2,2,2,2,2,2,3,3,3,3,3,4|0,0,4,14,30,41,50,55,59,64,74,83,90,93,97,100|0,2,2,2,2,2,2,2,2|0,0,7,46,83,92,96,100,100&chco=ff9900,1a00ff,ff00e6,80ff00,00e6ff,fae30a,BE81F7,9f5734,000000,ff0000,3090c0,477248f,ababab,7b9f34,00ff00,0000ff,9900ff,405090,051290,f3e000,9030f0,f03060,e0a030&chxt=x,y,x,y&chxl=2:||Duration+in+ms||3:||%25|&chdl=CF+Erin|CF+Erin+IPv6|CF+Ram|CF+Ram+IPv6|HE+1|HE+2|HE+2+IPv6|HE+3|HE+3+IPv6|HE+4|HE+4+IPv6|HE+5|HE+5+IPv6|Linode+1|Linode+1+IPv6|Linode+2|Linode+2+IPv6|Linode+3|Linode+3+IPv6|Linode+4|Linode+4+IPv6|Linode+5|Linode+5+IPv6

Recommended configuration (fastest + nearest):
----------------------------------------------
nameserver 216.66.1.2      # HE 4
nameserver 216.218.131.2   # HE 2
nameserver 216.66.80.18    # HE 5

********************************************************************************
In this test, HE 4 is 3.2%: Faster
********************************************************************************

- Saving report to /tmp/namebench_2015-07-17_1851.html
- Saving detailed results to /tmp/namebench_2015-07-17_1851.csv
```
## FAQ

**Most of these are likely not relevant to this modified version.**

See http://code.google.com/p/namebench/wiki/FAQ for more recent updates.

1) What does 'NXDOMAIN Hijacking' mean?

  This means that the specific DNS server returns a false entry when a
  non-existent record is requested. This entry likely points to a website
  serving a 'Host not found' page with banner ads.

2) What does 'www.google.com. may be hijacked' mean?

  This means that when a user requests 'www.google.com', they are being
  silently redirected to another server. The page may look like it's run by
  Google, but it is instead being proxied through another server. For details,
  try using the host command. In this case, this particular IP server is
  redirecting all traffic to http://google.navigation.opendns.com/

  % host www.google.com. 208.67.220.220
  Using domain server:
  Name: 208.67.220.220
  Address: 208.67.220.220#53
  Aliases:

  www.google.com is an alias for google.navigation.opendns.com.
  google.navigation.opendns.com has address 208.67.217.230
  google.navigation.opendns.com has address 208.67.217.231


3) What does 'google.com. may be hijacked' mean?

  The same as above, but it is a rarer condition as it breaks http://google.com/

4) What does 'thread.error: can't start new thread' mean?

  It means you are using too many threads. Try restarting namebench.py with -j8

5) What does 'unhealthy: TestWwwGoogleComResponse <class 'dns.exception.Timeout'>' mean?

  It means the specified nameserver was too slow to answer you. If all of your
  nameservers are timing out, try restarting namebench.py with -Y 4
