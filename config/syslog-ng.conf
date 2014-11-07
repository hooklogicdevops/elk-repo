@version: 3.3
@include "scl.conf"

# Syslog-ng configuration file, compatible with default Debian syslogd
# installation.

# First, set some global options.
options {       chain_hostnames(off);
                flush_lines(0);
                use_dns(no);
                use_fqdn(no);
                owner("root");
                group("adm");
                perm(0640);
                stats_freq(0);
                bad_hostname("^gconfd$");
                normalize_hostnames(yes);
                keep_hostname(no);
                create_dirs(yes);
                };

########################
# Sources
########################
#all messages arriving via tcp port 1000
source s_tcp {
        tcp(ip(0.0.0.0) port (1000) max-connections(500));
        };

########################
# Destinations
########################
#destination d_tcp { file("/var/log/syslog-ng/tcp.log"); };
destination d_logstash {
        tcp("127.0.0.1" port(6379));
};

########################
# Log paths
########################
# log statements are processed in order.
# messages are sent to each matching log statement, by default. see chapter 8 of the Syslog-ng 3.3 admin guide

log { source(s_tcp);
      destination(d_logstash);
};


###
# Include all config files in /etc/syslog-ng/conf.d/
###
@include "/etc/syslog-ng/conf.d/"