acct-opennebula-sensor
======================

An accounting sensor for opennebula. It takes the JSON output of the oneacct command as input and outputs usage records.

Its main purpose is to be used as a source of usage record for the SSM based accounting infrastructure of the EGI project.

Usage:

Usage: opennebulaSensorMain.rb [OPTIONS]
    -v, --verbose                    Output more information
    -U, --URI uri                    URI to contact
    -r, --resourceName resourceName  Name of resource, e.g. BDII siteName
    -d, --dir dir                    outpudDir for ssm files
    -L, --Limit limit                number of record per output file with ssmfile publisher
    -P, --Publisher type             Publisher type {ssm,ssmfile,XML,JSON,ActiveResource}
    -F, --File file                  File containing the output of oneacct --json command
    -t, --token token                Authorization token (needed only with FAUST ActiveResource backend). Must be requested to the service administrator
    -h, --help                       Print this screen