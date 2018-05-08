## sample_apache-log

Sample log files for playground.

## How they were created?

Those log files were generated based on the [NASA-HTTP](http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html).
The original log file can freely be redistributed.

 > Restrictions
 > The traces may be freely redistributed.

`fraud.log.gz` is prepared by @greymd.

```
$ mkdir log ## If necessary
$ cd log
$ zcat ../orig/*.gz | perl -ple '$m=int(rand(12));$d=sprintf("%02d", int(rand(28))+1);s/\[\d\d\/...\/\d{4}(:\d{2}:\d{2}:\d{2} -0400)\]/"[$d\/@{[qw<Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec>[$m]]}\/2017$1]"/e;s/$/" 2017@{[sprintf(\"%02d\",$m + 1)]}$d"/e' | perl -anle '@m=split(/\./, $F[0]); $F[0] = $m[0].".example";print "@F"' | awk '{f=$NF;NF=NF-1; print $0 > f}'
$ ls -U | perl -nle '$d = $_; $d =~ s/..$//; print "mkdir $d; mv $_ $d/access.log.$_"' | sh
```

## Restrictions

Sample files may be freely redistributed same as original traces.
