# utl-highlight-sashelp.class-and-enter-avgby-sex-age-on-command-line-for-proc-means
Highlight sashelp.class and enter avgby sex age on command line for proc means 

    %let pgm=utl-highlight-sashelp.class-and-enter-avgby-sex-age-on-command-line-for-proc-means;

    Highlight sashelp.class and enter avgby sex age on command line for proc means

    This only works in the 1980s classic unenhanced editor

    github
    https://tinyurl.com/2p97ebwm
    https://github.com/rogerjdeangelis/utl-highlight-sashelp.class-and-enter-avgby-sex-age-on-command-line-for-proc-means

    Performance package
    https://tinyurl.com/5f4m65nv
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories/blob/master/utl_perpac.sas

    * to compile the macros in the wor directory;
    filename perpac url
      'https://raw.githubusercontent.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories/master/utl_perpac.sas';
    %inc perpac;

    /*                                             _
      ___ ___  _ __ ___  _ __ ___   __ _ _ __   __| |
     / __/ _ \| `_ ` _ \| `_ ` _ \ / _` | `_ \ / _` |
    | (_| (_) | | | | | | | | | | | (_| | | | | (_| |
     \___\___/|_| |_| |_|_| |_| |_|\__,_|_| |_|\__,_|

    */

    Just highlight sashelp.class in 1980s editor and type svgby sex age (IBM ISPF editor had less wasted space)
    Some fancy editors wan you to program in a postage stamp?

    +-----+-----------------------------------+
    | sas | SAS (untitled)                    |--> You can recover this useless banner real estate but other things beak
    |-----+                                   |    Double wide banner?
    | File Edit View Tools Run Solutions .. . |
    +======================================+==+    -awscontrol notitle (this will turn it off)
    | Program editor avgby.sas             |  |
    +--------------------------------------+--+
    |  Command ===> avgby sex age          |  |
    |                                      |  |
    |  00001   data class;                 |  |
    |  00002      set SASHELP.CLASS ;      |--|
    |  00003      seq=_n_;                 |--|--> You can rmove the vertical scroll ar but other things break
    |  00004   run;quit;                   |  |    Scrool eheel fais (Probably a result of OO programmind)
    |  00005                               |  |
    |  ....                                |  |
    ---------------------------------------+--+--> You can eliminate the horizontal scroll bar
                                                   Substitute function ket "F3 left 3"

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    This will appear in output window

    -- MEANS of age by sex for dataset SASHELP.CLASS 30JAN2022:12:05:37 --

    Analysis Variable : AGE

              N             N                                                             Lower                Upper
     SEX    Obs     N    Miss             Sum            Mean         Std Dev   Minimum   Quartile    Median   Quartile   Maximum
     -----------------------------------------------------------------------------------------------------------------------------
     F        9     9       0     119.0000000      13.2222222       1.3944334      11.0      12.0      13.0      14.0      15.0
     M       10    10       0     134.0000000      13.4000000       1.6465452      11.0      12.0      13.5      15.0      16.0
     -----------------------------------------------------------------------------------------------------------------------------


    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    %macro avgby /cmd parmbuff
       des="highlight dataset and type sex age to get proc means by sex for age";
       %symdel argd arg1 arg2 / nowarn;
       %let arg1=%scan(&syspbuff,1,%str( ));
       %let arg2=%scan(&syspbuff,2,%str( ));
       store;note;notesubmit '%avgbya;';
       run;
    %mend avgby;

    %macro avgbya;
       filename clp clipbrd ;
       data _null_;
         infile clp;
         input;
         put _infile_;
         call symputx('argd',_infile_);
         call symputx("__dtetym",put(datetime(),datetime23.));
       run;
       dm "out;clear;";
       options nocenter;
       footnote;
       title1 "-- MEANS of &arg2 by &arg1 for dataset &argd &__dtetym --";
       proc means data=&argd  n nmiss sum mean std min q1 median q3 max;
       class &arg1;
       var &arg2.;
       run;
       title;
       dm "out;top;";
    %mend avgbya;

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
