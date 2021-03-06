acct-opennebula-sensor
======================

An accounting sensor for opennebula. It takes the JSON output of the oneacct command as input and outputs usage records.

Its main purpose is to be used as a source of usage record for the SSM based accounting infrastructure of the EGI project.

Usage:


opennebulaSensorMain.rb [OPTIONS]

    -v, --verbose                    Output more information
    -U, --URI uri                    URI to contact
    -r, --resourceName resourceName  Name of resource, e.g. BDII siteName
    -d, --dir dir                    outpudDir for ssm files
    -L, --Limit limit                number of record per output file with ssmfile publisher
    -P, --Publisher type             Publisher type {ssm,ssmfile,XML,JSON,ActiveResource}
    -F, --File file                  File containing the output of oneacct --json command
    -t, --token token                Authorization token (needed only with FAUST ActiveResource backend). Must be requested to the service administrator
    -h, --help                       Print this screen



The configuration for XML-RPC opennebula API credentials can be set in file mon_config.rb

Usage example: 

In cron:

DATE=`/bin/date +%Y-%m-01`

0,15,30,45 * * * * oneadmin export ONE_LOCATION=/home/cloudadm/prod/one/one ; export PATH=$ONE_LOCATION/bin:$PATH ; export LD_LIBRARY_PATH=$ONE_LOCATION/lib:$LD_LIBRARY_PATH ; export ONE_AUTH=$ONE_LOCATION/var/.one/one_auth ; oneacct -s "${DATE}" --json > /tmp/oneacctout.json.tmp 2> /dev/null ; mv /tmp/oneacctout.json.tmp /tmp/oneacctout.json

10,25,40,55 * * * * cloudadm cd /home/cloudadm/devel/faust-andrea/acct-opennebula-sensor; ./opennebulaSensorMain.rb -f /tmp/oneacctout.json -P ssmfile -d /var/spool/apel/outgoing/deadbeef/ -r INFN-TORINO -L 100 >/tmp/faust.log 2>&1

0,20,40 * * * * root ssmsend > /dev/null 2>&1

ssmsend is from apel ssm tools.