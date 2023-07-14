# utl-transpose-fat-to-skinny-pivot-longer-in-sas-wps-r-pythonv
Transpose fat to skinny pivot longer in sas wps r python 
    %let pgm=utl-transpose-fat-to-skinny-pivot-longer-in-sas-wps-r-python;

    Transpose fat to skinny pivot longer in sas wps r python

    github
    https://tinyurl.com/25kf8a9y
    https://github.com/rogerjdeangelis/utl-transpose-fat-to-skinny-pivot-longer-in-sas-wps-r-pythonv

    https://tinyurl.com/39bku4dx
    https://github.com/rogerjdeangelis/utl-classic-transpose-by-index-variableid-and-value-in-sas-r-and-python

      SOLUTIONS

          1. R native code
          2. wps/sas untranspose (a one liner in wps and sas)
             untranspose(data=sd1.have,out=want,by=STATIONHCTREATMENT,delimiter=_,id=month,var=AVGSTD)
          3. wps/sas proc sql (just as easy to do with a datastep)
          4. R sql
             However, I use wps to generate the sql code script for r sqldf function
          5. Python sql
             However, I use wps to generate the sql code script for r sqldf function

    https://stackoverflow.com/questions/76665964/dataset-transformation-from-gather-to-pivot-longer

    It is fairly easy in WPS with array and do_over macros to generate the SQL code

    This is the ql code, may not be as slow as you think, depends on the compiler

              select station ,hc ,treatment ,AVG_0  as avg ,STD_0  as std from have
    union corr select station ,hc ,treatment ,AVG_12 as avg ,STD_12 as std from have
    union corr select station ,hc ,treatment ,AVG_24 as avg ,STD_24 as std from have
    union corr select station ,hc ,treatment ,AVG_36 as avg ,STD_36 as std from have
    union corr select station ,hc ,treatment ,AVG_48 as avg ,STD_48 as std from have
    union corr select station ,hc ,treatment ,AVG_60 as avg ,STD_60 as std from have
    union corr select station ,hc ,treatment ,AVG_72 as avg ,STD_72 as std from have

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    libname sd1 "d:/sd1";

    options validvarname=upcase;

    data sd1.have;informat
    STATION $5.
    HC $14.
    TREATMENT $7.
    AVG_0 8.
    AVG_12 8.
    AVG_24 8.
    AVG_36 8.
    AVG_48 8.
    AVG_60 8.
    AVG_72 8.
    STD_0 8.
    STD_12 8.
    STD_24 8.
    STD_36 8.
    STD_48 8.
    STD_60 8.
    STD_72 8.
    ;input
    STATION HC TREATMENT AVG_0 AVG_12 AVG_24 AVG_36 AVG_48 AVG_60 AVG_72
     STD_0 STD_12 STD_24 STD_36 STD_48 STD_60 STD_72;
    cards4;
    Stn01 Alkanes Control 6.62 6.47 6.39 6.38 6.49 6.22 6.84 0.12 0.1 0.25 0.47 0.6 0.82 0.02
    Stn11 Alkanes Control 6.82 7.33 8.1 8.06 7.9 7.96 7.15 0.98 0.39 0.58 0.63 0.31 0.61 0.4
    Stn20 Alkanes Control 0 0 0 3.82 0 6.56 7.49 0 0 0 3.35 0 0.22 0.2
    Stn01 AlkylatedPAHs Control 0 0 0 0 0 0 0 0 0 0 0 0 0 0
    Stn11 AlkylatedPAHs Control 0 2.61 0 2.25 0 0 0 0 4.52 0 3.9 0 0 0
    Stn20 AlkylatedPAHs Control 0 0 0 0 0 0 0 0 0 0 0 0 0 0
    Stn01 PAHs Control 0 0 0 0 0 0 0 0 0 0 0 0 0 0
    Stn11 PAHs Control 0 1.86 3.51 4.86 4.89 5.45 4.72 0 3.23 3.08 0.32 0.36 0.66 0.32
    Stn20 PAHs Control 0 0 0 0 0 0 0 0 0 0 0 0 0 0
    Stn01 Alkanes Diesel 9.73 9.8 9.55 9.04 9.24 9.15 9.24 1.35 1.18 1.16 1.33 0.14 0.57 0.56
    Stn11 Alkanes Diesel 9.92 9.94 9.92 9.13 9.47 9.46 8.46 0.42 0.98 0.41 0.28 0.88 1.03 0.89
    Stn20 Alkanes Diesel 9.98 9.8 9.35 9.4 8.28 8.05 9.89 0.29 0.26 0.43 1.63 0.29 0.31 0.49
    Stn01 AlkylatedPAHs Diesel 7.96 8.66 7.78 7.38 7.23 7 6.78 1.04 0.18 0.19 0.16 0.5 0.16 0.61
    Stn11 AlkylatedPAHs Diesel 6.71 9.32 8.27 7.15 7.27 5.86 4.01 0.86 0.49 0.39 0.31 0.49 1.3 3.48
    Stn20 AlkylatedPAHs Diesel 6.9 8.39 7.76 7.48 6.74 1.95 4.03 0.45 0.13 0.09 0.47 0.35 3.38 3.51
    Stn01 PAHs Diesel 3.97 6.26 5.64 4.77 4.55 1.48 0 3.44 0.37 0.24 0.1 0.15 2.56 0
    Stn11 PAHs Diesel 2.95 7.22 6.69 6.24 6.21 5.93 3.56 2.56 0.16 0.15 0.13 0.18 0.27 3.09
    Stn20 PAHs Diesel 0 6.44 5.64 4.83 3 0 0 0 0.06 0.07 0.12 2.59 0 0
    Stn01 Alkanes Heidrun 9.58 8.93 8.28 8.48 8.92 8.78 8.42 0.88 0.03 0.27 0.64 1 0.43 0.82
    Stn11 Alkanes Heidrun 9.73 8.49 8.84 8.65 8.97 8.56 7.55 0.23 0.4 0.06 0.1 0.08 0.07 1.5
    Stn20 Alkanes Heidrun 9.79 0 1.68 3.56 3.44 7.31 8.21 0.09 0 2.91 3.08 2.98 0.23 0.06
    Stn01 AlkylatedPAHs Heidrun 9.37 9.08 9.26 8.91 8.79 8.63 5.38 1.72 0.29 0.12 0.35 0.2 0.48 4.69
    Stn11 AlkylatedPAHs Heidrun 9.78 9.42 9.99 9.52 9.28 8.49 8.02 0.23 0.15 0.24 0.16 0.15 0.27 0.14
    Stn20 AlkylatedPAHs Heidrun 9.89 9.7 9.2 8.34 7.85 7.1 7.46 0.1 0.11 0.05 0.09 0.18 0.39 0.3
    Stn01 PAHs Heidrun 7 8.58 7.93 7.32 7.07 7.23 4.57 1.79 0.08 0.15 0.18 0.24 0.25 3.96
    Stn1 1PAHs Heidrun 8.49 9.1 8.66 8.31 8.04 7.77 7.42 0.23 0.12 0.3 0.14 0.14 0.15 0.19
    Stn20 PAHs Heidrun 8.49 8.47 8.04 7.58 7.17 6.62 6.6 0.09 0.08 0.07 0.02 0.13 0.2 0.06
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Some character fields shortened to fit                                                                                */
    /*                                                                                                                        */
    /* Up to 40 obs from last table WORK.HAVE total obs=27 12MAY2023:09:17:44                                                 */
    /*                                                                                                                        */
    /*   STATION HC TREATMENT AVG_0 AVG_12 AVG_24 AVG_36 AVG_48 AVG_60 AVG_72 STD_0 STD_12 STD_24 STD_36 STD_48 STD_60 STD_72 */
    /*                                                                                                                        */
    /*  1   Stn01 Alka Contro  6.62   6.47   6.39   6.38   6.49   6.22   6.84   0.12   0.10   0.25   0.47   0.60  0.82  0.02  */
    /*  2   Stn11 Alka Contro  6.82   7.33   8.10   8.06   7.90   7.96   7.15   0.98   0.39   0.58   0.63   0.31  0.61  0.40  */
    /*  3   Stn20 Alka Contro  0.00   0.00   0.00   3.82   0.00   6.56   7.49   0.00   0.00   0.00   3.35   0.00  0.22  0.20  */
    /*  4   Stn01 Alky Contro  0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00  0.00  0.00  */
    /*  5   Stn11 Alky Contro  0.00   2.61   0.00   2.25   0.00   0.00   0.00   0.00   4.52   0.00   3.90   0.00  0.00  0.00  */
    /*  6   Stn20 Alky Contro  0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00  0.00  0.00  */
    /*  7   Stn01 PAHs Contro  0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00  0.00  0.00  */
    /*  8   Stn11 PAHs Contro  0.00   1.86   3.51   4.86   4.89   5.45   4.72   0.00   3.23   3.08   0.32   0.36  0.66  0.32  */
    /*  9   Stn20 PAHs Contro  0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00   0.00  0.00  0.00  */
    /* 10   Stn01 Alka Diesel  9.73   9.80   9.55   9.04   9.24   9.15   9.24   1.35   1.18   1.16   1.33   0.14  0.57  0.56  */
    /* 11   Stn11 Alka Diesel  9.92   9.94   9.92   9.13   9.47   9.46   8.46   0.42   0.98   0.41   0.28   0.88  1.03  0.89  */
    /* 12   Stn20 Alka Diesel  9.98   9.80   9.35   9.40   8.28   8.05   9.89   0.29   0.26   0.43   1.63   0.29  0.31  0.49  */
    /* 13   Stn01 Alky Diesel  7.96   8.66   7.78   7.38   7.23   7.00   6.78   1.04   0.18   0.19   0.16   0.50  0.16  0.61  */
    /* 14   Stn11 Alky Diesel  6.71   9.32   8.27   7.15   7.27   5.86   4.01   0.86   0.49   0.39   0.31   0.49  1.30  3.48  */
    /* 15   Stn20 Alky Diesel  6.90   8.39   7.76   7.48   6.74   1.95   4.03   0.45   0.13   0.09   0.47   0.35  3.38  3.51  */
    /* 16   Stn01 PAHs Diesel  3.97   6.26   5.64   4.77   4.55   1.48   0.00   3.44   0.37   0.24   0.10   0.15  2.56  0.00  */
    /* 17   Stn11 PAHs Diesel  2.95   7.22   6.69   6.24   6.21   5.93   3.56   2.56   0.16   0.15   0.13   0.18  0.27  3.09  */
    /* 18   Stn20 PAHs Diesel  0.00   6.44   5.64   4.83   3.00   0.00   0.00   0.00   0.06   0.07   0.12   2.59  0.00  0.00  */
    /* 19   Stn01 Alka Heidru  9.58   8.93   8.28   8.48   8.92   8.78   8.42   0.88   0.03   0.27   0.64   1.00  0.43  0.82  */
    /* 20   Stn11 Alka Heidru  9.73   8.49   8.84   8.65   8.97   8.56   7.55   0.23   0.40   0.06   0.10   0.08  0.07  1.50  */
    /* 21   Stn20 Alka Heidru  9.79   0.00   1.68   3.56   3.44   7.31   8.21   0.09   0.00   2.91   3.08   2.98  0.23  0.06  */
    /* 22   Stn01 Alky Heidru  9.37   9.08   9.26   8.91   8.79   8.63   5.38   1.72   0.29   0.12   0.35   0.20  0.48  4.69  */
    /* 23   Stn11 Alky Heidru  9.78   9.42   9.99   9.52   9.28   8.49   8.02   0.23   0.15   0.24   0.16   0.15  0.27  0.14  */
    /* 24   Stn20 Alky Heidru  9.89   9.70   9.20   8.34   7.85   7.10   7.46   0.10   0.11   0.05   0.09   0.18  0.39  0.30  */
    /* 25   Stn01 PAHs Heidru  7.00   8.58   7.93   7.32   7.07   7.23   4.57   1.79   0.08   0.15   0.18   0.24  0.25  3.96  */
    /* 26   Stn11 PAHs Heidru  8.49   9.10   8.66   8.31   8.04   7.77   7.42   0.23   0.12   0.30   0.14   0.14  0.15  0.19  */
    /* 27   Stn20 PAHs Heidru  8.49   8.47   8.04   7.58   7.17   6.62   6.60   0.09   0.08   0.07   0.02   0.13  0.20  0.06  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                      _   _                           _
    / |  _ __   _ __   __ _| |_(_)_   _____    ___ ___   __| | ___
    | | | `__| | `_ \ / _` | __| \ \ / / _ \  / __/ _ \ / _` |/ _ \
    | | | |    | | | | (_| | |_| |\ V /  __/ | (_| (_) | (_| |  __/
    |_| |_|    |_| |_|\__,_|\__|_| \_/ \___|  \___\___/ \__,_|\___|

    */

    /*---- proc datasets is on shf f6 function key no need to type it        ----*/
    /*---- Could save code in profile then a in prefix and copy on command   ----*/
    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    %utl_submit_wps64('
    libname sd1 "d:/sd1";
    proc r;
    export data=sd1.have r=have;
    submit;
    library(tidyverse);
    want<-pivot_longer(have, -c(STATION, HC, TREATMENT),
                 names_pattern = "(.*)_(.*)",
                 names_to = c(".value", "Var"));
    endsubmit;
    import data=sd1.want r=want;
    proc print data=sd1.want;
    run;quit;
    ');

    proc print data=sd1.want;
    run;quit;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* The WPS System                                                                                                         */
    /*                                                                                                                        */
    /* Obs    STATION         HC          TREATMENT    VAR    AVG     STD                                                     */
    /*                                                                                                                        */
    /*   1     Stn01     Alkanes           Control     0      6.62    0.12                                                    */
    /*   2     Stn01     Alkanes           Control     12     6.47    0.10                                                    */
    /*   3     Stn01     Alkanes           Control     24     6.39    0.25                                                    */
    /*   4     Stn01     Alkanes           Control     36     6.38    0.47                                                    */
    /*   5     Stn01     Alkanes           Control     48     6.49    0.60                                                    */
    /*   6     Stn01     Alkanes           Control     60     6.22    0.82                                                    */
    /*   7     Stn01     Alkanes           Control     72     6.84    0.02                                                    */
    /*   8     Stn11     Alkanes           Control     0      6.82    0.98                                                    */
    /*   9     Stn11     Alkanes           Control     12     7.33    0.39                                                    */
    /*  10     Stn11     Alkanes           Control     24     8.10    0.58                                                    */
    /*  11     Stn11     Alkanes           Control     36     8.06    0.63                                                    */
    /*  12     Stn11     Alkanes           Control     48     7.90    0.31                                                    */
    /*  13     Stn11     Alkanes           Control     60     7.96    0.61                                                    */
    /*  14     Stn11     Alkanes           Control     72     7.15    0.40                                                    */
    /*  15     Stn20     Alkanes           Control     0      0.00    0.00                                                    */
    /*  16     Stn20     Alkanes           Control     12     0.00    0.00                                                    */
    /*  17     Stn20     Alkanes           Control     24     0.00    0.00                                                    */
    /*  18     Stn20     Alkanes           Control     36     3.82    3.35                                                    */
    /*  19     Stn20     Alkanes           Control     48     0.00    0.00                                                    */
    /*  20     Stn20     Alkanes           Control     60     6.56    0.22                                                    */
    /*  21     Stn20     Alkanes           Control     72     7.49    0.20                                                    */
    /*  ....                                                                                                                  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/
    /*___                          __                           _
    |___ \  __      ___ __  ___   / /__  __ _ ___   _   _ _ __ | |_ _ __ __ _ _ __  ___ _ __   ___  ___  ___
      __) | \ \ /\ / / `_ \/ __| / / __|/ _` / __| | | | | `_ \| __| `__/ _` | `_ \/ __| `_ \ / _ \/ __|/ _ \
     / __/   \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ | |_| | | | | |_| | | (_| | | | \__ \ |_) | (_) \__ \  __/
    |_____|   \_/\_/ | .__/|___/_/ |___/\__,_|___/  \__,_|_| |_|\__|_|  \__,_|_| |_|___/ .__/ \___/|___/\___|

    */

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    %untranspose(data=sd1.have, out=want, by=STATION HC TREATMENT, delimiter=_,  id=month, var=AVG STD)

    /*
    __      ___ __  ___
    \ \ /\ / / `_ \/ __|
     \ V  V /| |_) \__ \
      \_/\_/ | .__/|___/
             |_|
    */

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    %utl_wpsbegin;
    parmcards4;
    libname sd1 "d:/sd1";
    %untranspose(data=sd1.have, out=sd1.want, by=STATION HC TREATMENT, delimiter=_,  id=month, var=AVG STD);
    proc print data=sd1.want;
    run;quit;
    ;;;;
    %utl_wpsend;
    run;quit;



    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  The WPS System                                                                                                        */
    /*                                                                                                                        */
    /*  Obs    STATION         HC          TREATMENT       MONTH    AVG     STD                                               */
    /*                                                                                                                        */
    /*    1     Stn01     Alkanes           Control            0    6.62    0.12                                              */
    /*    2     Stn01     Alkanes           Control           12    6.47    0.10                                              */
    /*    3     Stn01     Alkanes           Control           24    6.39    0.25                                              */
    /*    4     Stn01     Alkanes           Control           36    6.38    0.47                                              */
    /*    5     Stn01     Alkanes           Control           48    6.49    0.60                                              */
    /*    6     Stn01     Alkanes           Control           60    6.22    0.82                                              */
    /*    7     Stn01     Alkanes           Control           72    6.84    0.02                                              */
    /*    8     Stn11     Alkanes           Control            0    6.82    0.98                                              */
    /*    9     Stn11     Alkanes           Control           12    7.33    0.39                                              */
    /*   10     Stn11     Alkanes           Control           24    8.10    0.58                                              */
    /*   11     Stn11     Alkanes           Control           36    8.06    0.63                                              */
    /*   12     Stn11     Alkanes           Control           48    7.90    0.31                                              */
    /*   13     Stn11     Alkanes           Control           60    7.96    0.61                                              */
    /*   14     Stn11     Alkanes           Control           72    7.15    0.40                                              */
    /*   15     Stn20     Alkanes           Control            0    0.00    0.00                                              */
    /*   16     Stn20     Alkanes           Control           12    0.00    0.00                                              */
    /*   17     Stn20     Alkanes           Control           24    0.00    0.00                                              */
    /*   18     Stn20     Alkanes           Control           36    3.82    3.35                                              */
    /*   19     Stn20     Alkanes           Control           48    0.00    0.00                                              */
    /*   20     Stn20     Alkanes           Control           60    6.56    0.22                                              */
    /*   21     Stn20     Alkanes           Control           72    7.49    0.20                                              */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                         __                                               _
    |___ /  __      ___ __  ___   / /__  __ _ ___   _ __  _ __ ___   ___  ___  __ _| |
      |_ \  \ \ /\ / / `_ \/ __| / / __|/ _` / __| | `_ \| `__/ _ \ / __|/ __|/ _` | |
     ___) |  \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ | |_) | | | (_) | (__ \__ \ (_| | |
    |____/    \_/\_/ | .__/|___/_/ |___/\__,_|___/ | .__/|_|  \___/ \___||___/\__, |_|
                     |_|                           |_|                           |_|
    */

    %array(_AVG,values=%varlist(sd1.have,keep=AVG:));
    %array(_STD,values=%varlist(sd1.have,keep=STD:));

    %put xxxx &=_avg3;
    %put xxxx &=_avgn;

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    proc sql;
      create
        table sd1.want as
      %do_over(_avg _std, phrase=%str(
        select
          STATION
         ,HC
         ,TREATMENT
         ,scan("?_avg",2,"_") as month
         ,?_avg as avg
         ,?_std as std
        from
          sd1.have
      ),between=union corr)
    ;quit;

    /*----  sample on generating the dode                                    ----*/
    data _null_;
      put
      %do_over(_avg _std,phrase=put ",scan('?_avg',2,'_') as month,?_avg as avg,?_std as std)" / );
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Generated code                                                                                                         */
    /*                                                                                                                        */
    /* ,scan('AVG_0',2,'_')  as month,AVG_0  as avg,STD_0 as std)                                                             */
    /* ,scan('AVG_12',2,'_') as month,AVG_12 as avg,STD_12 as std)                                                            */
    /* ,scan('AVG_24',2,'_') as month,AVG_24 as avg,STD_24 as std)                                                            */
    /* ,scan('AVG_36',2,'_') as month,AVG_36 as avg,STD_36 as std)                                                            */
    /* ,scan('AVG_48',2,'_') as month,AVG_48 as avg,STD_48 as std)                                                            */
    /* ,scan('AVG_60',2,'_') as month,AVG_60 as avg,STD_60 as std)                                                            */
    /* ,scan('AVG_72',2,'_') as month,AVG_72 as avg,STD_72 as std)                                                            */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*
    __      ___ __  ___
    \ \ /\ / / `_ \/ __|
     \ V  V /| |_) \__ \
      \_/\_/ | .__/|___/
             |_|
    */

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    %utl_wpsbegin;
    parmcards4;
    %utlopts;
    options validvarname=any;
    libname sd1 "d:/sd1";
    %array(_AVG,values=%varlist(sd1.have,keep=AVG:));
    %array(_STD,values=%varlist(sd1.have,keep=STD:));
    proc sql;
      create
        table sd1.want as
      %do_over(_avg _std, phrase=%str(
        select
          STATION
         ,HC
         ,TREATMENT
         ,scan("?_avg",2,"_") as month
         ,?_avg as avg
         ,?_std as std
        from
          sd1.have
      ),between=union corr)
    ;quit;
    proc print data=sd1.want;
    run;quit;
    ;;;;
    %utl_wpsend;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  The WPS System                                                                                                        */
    /*                                                                                                                        */
    /*  Obs    STATION         HC          TREATMENT    month    avg     std                                                  */
    /*                                                                                                                        */
    /*    1     Stn01     Alkanes           Control      0       6.62    0.12                                                 */
    /*    2     Stn01     Alkanes           Control      12      6.47    0.10                                                 */
    /*    3     Stn01     Alkanes           Control      24      6.39    0.25                                                 */
    /*    4     Stn01     Alkanes           Control      36      6.38    0.47                                                 */
    /*    5     Stn01     Alkanes           Control      48      6.49    0.60                                                 */
    /*    6     Stn01     Alkanes           Control      60      6.22    0.82                                                 */
    /*    7     Stn01     Alkanes           Control      72      6.84    0.02                                                 */
    /*    8     Stn01     Alkanes           Diesel       0       9.73    1.35                                                 */
    /*    9     Stn01     Alkanes           Diesel       12      9.80    1.18                                                 */
    /*   10     Stn01     Alkanes           Diesel       24      9.55    1.16                                                 */
    /*   11     Stn01     Alkanes           Diesel       36      9.04    1.33                                                 */
    /*   12     Stn01     Alkanes           Diesel       48      9.24    0.14                                                 */
    /*   13     Stn01     Alkanes           Diesel       60      9.15    0.57                                                 */
    /*   14     Stn01     Alkanes           Diesel       72      9.24    0.56                                                 */
    /*   15     Stn01     Alkanes           Heidrun      0       9.58    0.88                                                 */
    /*   16     Stn01     Alkanes           Heidrun      12      8.93    0.03                                                 */
    /*   17     Stn01     Alkanes           Heidrun      24      8.28    0.27                                                 */
    /*   18     Stn01     Alkanes           Heidrun      36      8.48    0.64                                                 */
    /*   19     Stn01     Alkanes           Heidrun      48      8.92    1.00                                                 */
    /*   20     Stn01     Alkanes           Heidrun      60      8.78    0.43                                                 */
    /*   21     Stn01     Alkanes           Heidrun      72      8.42    0.82                                                 */
    /*   ....                                                                                                                 */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _                      _
    | || |    _ __   ___  __ _| |
    | || |_  | `__| / __|/ _` | |
    |__   _| | |    \__ \ (_| | |
       |_|   |_|    |___/\__, |_|
                            |_|
    */

    options validvarname=upcase;
    proc datasets lib=sd1 nolist nodetails;delete havsql want; run;quit;

    %utl_wpsbeginx;
    parmcards4;
    libname sd1 "d:/sd1";
    %array(_AVG,values=%varlist(sd1.have,keep=AVG:));
    %array(_STD,values=%varlist(sd1.have,keep=STD:));
    %put &=_std4;
    %put &=_stdn;
    filename tmp "d:/txt/sqlcde.txt" lrecl=4096 recfm=v;;
    data sd1.havsql(keep=sqlcde);
     length sqlcde $4096;
     sqlCde=compbl("
         %do_over(_avg _std, phrase=%str(
          select
            station
           ,hc
           ,treatment
           ,?_avg as avg
           ,?_std as std
          from
            have
          ),between=union all)");
    putlog "I am in WPS";
    putlog sqlCde;
    run;quit;

    proc r;
     export data=sd1.havsql r=havsql;
     export data=sd1.have   r=have;
     submit;
     library(sqldf);
     want<-sqldf(havsql$SQLCDE);
     head(want);
    endsubmit;
    import data=sd1.want r=want;
    run;quit;

    ;;;;
    %utl_wpsendx;

    proc print data=sd1.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  The WPS System                                                                                                        */
    /*                                                                                                                        */
    /*    STATION            HC TREATMENT  avg  std                                                                           */
    /*  1   Stn01       Alkanes   Control 6.62 0.12                                                                           */
    /*  2   Stn11       Alkanes   Control 6.82 0.98                                                                           */
    /*  3   Stn20       Alkanes   Control 0.00 0.00                                                                           */
    /*  4   Stn01 AlkylatedPAHs   Control 0.00 0.00                                                                           */
    /*  5   Stn11 AlkylatedPAHs   Control 0.00 0.00                                                                           */
    /*  6   Stn20 AlkylatedPAHs   Control 0.00 0.00                                                                           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                _   _                             _
    | ___|   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
    |___ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */

    title;footnote;
    options validvarname=upcase;
    proc datasets lib=sd1 nolist nodetails;delete havsql want; run;quit;

    %utl_wpsbeginx;
    parmcards4;
    libname sd1 "d:/sd1";
    %array(_AVG,values=%varlist(sd1.have,keep=AVG:));
    %array(_STD,values=%varlist(sd1.have,keep=STD:));
    %put &=_std4;
    %put &=_stdn;
    filename tmp "d:/txt/sqlcde.txt" lrecl=4096 recfm=v;;
    data sd1.havsql(keep=sqlcde);
     length sqlcde $4096;
     sqlCde=compbl("
         %do_over(_avg _std, phrase=%str(
          select
            station
           ,hc
           ,treatment
           ,?_avg as avg
           ,?_std as std
          from
            have
          ),between=union all)");
    putlog "I am in WPS";
    putlog sqlCde;
    run;quit;

    proc python;
    export data=sd1.havsql python=havsql;
    export data=sd1.have   python=have;
    submit;
    from os import path;
    import pandas as pd;
    import numpy as np;
    import textwrap3 as tw;
    from pandasql import sqldf;
    mysql = lambda q: sqldf(q, globals());
    from pandasql import PandaSQL;
    pdsql = PandaSQL(persist=True);
    sqlite3conn = next(pdsql.conn.gen).connection.connection;
    sqlite3conn.enable_load_extension(True);
    sqlite3conn.load_extension('c:/temp/libsqlitefunctions.dll');
    mysql = lambda q: sqldf(q, globals());
    havsql['SQLCDE'] = havsql['SQLCDE'].astype('string');
    cde = havsql['SQLCDE'].str.strip();
    want =pdsql(cde);;
    print(want);
    endsubmit;
    run;quit;
    ;;;;
    %utl_wpsendx;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* The WPS System                                                                                                         */
    /*                                                                                                                        */
    /* The PYTHON Procedure                                                                                                   */
    /*                                                                                                                        */
    /*     STATION              HC TREATMENT   avg   std                                                                      */
    /* 0     Stn01  Alkanes          Control  6.62  0.12                                                                      */
    /* 1     Stn11  Alkanes          Control  6.82  0.98                                                                      */
    /* 2     Stn20  Alkanes          Control  0.00  0.00                                                                      */
    /* 3     Stn01  AlkylatedPAHs    Control  0.00  0.00                                                                      */
    /* 4     Stn11  AlkylatedPAHs    Control  0.00  0.00                                                                      */
    /* ..      ...             ...       ...   ...   ...                                                                      */
    /* 184   Stn11  AlkylatedPAHs    Heidrun  8.02  0.14                                                                      */
    /* 185   Stn20  AlkylatedPAHs    Heidrun  7.46  0.30                                                                      */
    /* 186   Stn01  PAHs             Heidrun  4.57  3.96                                                                      */
    /* 187   Stn1   1PAHs            Heidrun  7.42  0.19                                                                      */
    /* 188   Stn20  PAHs             Heidrun  6.60  0.06                                                                      */
    /*                                                                                                                        */
    /* [189 rows x 5 columns]                                                                                                 */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
