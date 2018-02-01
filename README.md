# utl_detecting_structural_breaks_in_a_time_series
Detecting structural breaks in a time series. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Detecting structural breaks in a time series

    project
    https://goo.gl/PK7yk3
    https://github.com/rogerjdeangelis/utl_detecting_structural_breaks_in_a_time_series

    SAS Forum
    https://goo.gl/UbtDko
    https://communities.sas.com/t5/SAS-Forecasting-and-Econometrics/Detecting-structural-breaks-when-using-Panel-data/m-p/433125

    R solution
    https://goo.gl/qnjiRR
    https://pythonandr.com/2016/11/08/endogenously-detecting-structural-breaks-in-a-time-series-implementation-in-r/



    INPUT

     SD1.HAVE total obs=58

       YEAR    RICE

       1951     668
       1952     714
       1953     764
       1954     902
       ....     ...
       2006     2102
       2007     2131
       2008     2202


                      Plot of RICE*YEAR.  Symbol used is '+'.

           ---+---------+---------+---------+---------+---------+---------+---
      RICE |                                                                 |
      2250 +                                                                 +
           |                                                            +    |
           |                                                          ++     |
           |                                                      + +        |
      2000 +                                                    +    +       +
           |                                               +   +             |
           |                                              +  ++  +           |
           |                                                +                |
      1750 +                                          ++++         +         +
           |                                         +                       |
           |                                                                 |
           |                                      +                          |
      1500 +                                       +                         +
           |                                    ++  +                        |
           |                                                                 |
           |                              ++ ++                              |
      1250 +                            +      +                             +
           |                                                                 |
           |                       ++ +                                      |
           |                ++  +++  + + +  +                                |
      1000 +             ++                                                  +
           |           ++  +                                                 |
           |      + ++        ++                                             |
           |       +  +                                                      |
       750 +     +                                                           +
           |   ++                                                            |
           |                                                                 |
           |                                                                 |
       500 +                                                                 +
           |                                                                 |
           ---+---------+---------+---------+---------+---------+---------+---
            1950      1960      1970      1980      1990      2000      2010

                                          YEAR

    PROCESS (WORKING CODE)
    ======================

         WPS/PROC R

           ricex <- breakpoints(rice ~ 1);

    OUTPUT
    ======

      WORK.WANT total obs=5

          BREAKS
          ----
          1958
          1968
          1980
          1988
          1998


                         Plot of RICE*YEAR.  Symbol used is '+'.
              ---+---------+---------+---------+---------+---------+---------+---
         RICE |          |         |           |       |         |              |
         2250 +          |         |           |       |         |              +
              |          |         |           |       |         |         +    |
              |          |         |           |       |         |       ++     |
              |          |         |           |       |         |   + +        |
         2000 +          |         |           |       |         | +    +       +
              |          |         |           |       |      +  |+             |
              |          |         |           |       |     +  ++  +           |
              |          |         |           |       |       + |              |
         1750 +          |         |           |       | ++++    |    +         +
              |          |         |           |       |+        |              |
              |          |         |           |       |         |              |
              |          |         |           |     + |         |              |
         1500 +          |         |           |      +|         |              +
              |          |         |           |   ++  +         |              |
              |          |         |           |       |         |              |
              |          |         |         ++|++     |         |              |
         1250 +          |         |       +   |  +    |         |              +
              |          |         |           |       |         |              |
              |          |         |  ++ +     |       |         |              |
              |          |     ++  +++  + + +  +       |         |              |
         1000 +          |  ++     |           |       |         |              +
              |          |++  +    |           |       |         |              |
              |      + ++|       ++|           |       |         |              |
              |       +  +         |           |       |         |              |
          750 +     +    |         |           |       |         |              +
              |   ++     |         |           |       |         |              |
              |          |         |           |       |         |              |
              |          |         |           |       |         |              |
          500 +          |         |           |       |         |              +
              |          |         |           |       |         |              |
              ---+---------+---------+---------+---------+---------+---------+---
               1950      1960      1970      1980      1990      2000      2010
                                             YEAR

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have(label="1951 to 2008");
     retain year 1950;
     input rice @@;
     year=year+1;
     rice=round(rice,1);
    cards4;
    668 714 764 902 820 874 900 790 930 937
    1013 1028 931 1033 1078 862 863 1032
    1076 1073 1123 1141 1070 1151 1045 1235
    1089 1308 1328 1074 1336 1308 1231 1457
    1417 1552 1471 1465 1689 1745 1740 1751
    1744 1888 1911 1797 1882 1900 1921 1986
    1901 2079 1744 2077 1984 2102 2131 2202
    ;;;;
    run;quit;

    options ls=80 ps=40 nocenter;
    proc plot data=sd1.have;
    plot rice*year='+'/box;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    proc datasets lib=work kill;
    run;quit;

    %symdel breaks / nowarn;

    %utl_submit_wps64('
    libname sd1 sas7bdat "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    proc r;
    submit;
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
    library(xlsx);
    library(forecast);
    library(tseries);
    library(strucchange);
    library(haven);
    prod_df<-as.data.frame(read_sas("d:/sd1/have.sas7bdat"));
    rice <- ts(prod_df$RICE, start=c(1951, 1), end=c(2008, 1), frequency=1);
    png("d:/png/utl_detecting_structural_breaks_in_a_time_series.png");
    ricex <- breakpoints(rice ~ 1);
    want<-ricex$breakpoints;
    plot(ricex);
    plot(rice);
    lines(ricex);
    ci.rice <- confint(ricex);
    lines(ci.rice);
    endsubmit;
    import r=want  data=wrk.want;
    run;quit;
    ');

    proc sql;
     select put(1950+want,4.) into :breaks separated by " " from want
    ;quit;

    options ls=72 ps=40 nocenter;
    proc plot data=sd1.have;
    plot rice*year='+'/href=&breaks box;
    run;quit;

