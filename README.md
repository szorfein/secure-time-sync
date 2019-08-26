# Secure Time Synchronization

A simple bash script that securely syncs the time to the correct UTC time.

This script connects to a variety of websites and extracts the current UTC time from the http headers.

The website is randomly selected from a pool of carefully chosen websites.

The current websites in the pool are:

* The Tor Project
* The Tails website
* The Whonix website
* DuckDuckGo
* The EFF's website

The script can optionally connect to these websites over Tor and will connect to an onion service where possible.

If not using Tor, the script protects against https downgrade attacks by enforcing TLS with curl.

To use the script, download it, make it executable and run

    ./secure-time-sync.sh
    
To use it with Tor, run

    ./secure-time-sync.sh --use-tor
     
This will configure curl to use localhost on port 9050 as a socks proxy. Port 9050 is the default Tor SocksPort.

Debugging information (the selected website and extracted time) can be gotten by starting the script with the DEBUG_TS=1 environment variable.

    DEBUG_TS=1 ./secure-time-sync.sh
     
The script needs to be run as root so it can set the time.

To make this script run daily, you can configure a cron job to automatically run it.

This script doesn't support any timezones other than UTC.