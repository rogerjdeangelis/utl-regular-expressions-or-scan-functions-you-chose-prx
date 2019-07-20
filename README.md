# utl-regular-expressions-or-scan-functions-you-chose-prx
Regular expressions or scan functions you chose prx

    Regular expressions or scan functions you chose prx

    github
    https://tinyurl.com/y34hwotc
    https://github.com/rogerjdeangelis/utl-regular-expressions-or-scan-functions-you-chose-prx

    https://tinyurl.com/yyquw95z
    https://communities.sas.com/t5/New-SAS-User/Extracting-multiple-matched-pattern-from-dataset/m-p/575113

    SUGGESTED SOLUTIONS

          1  prxchange('s/.*(\d{2}(\s+|-)\w+(\s+|-)\d{2,4}).*/\1/', 1, term);
          2  prxchange('s/.*(\d{2}(\s+|-)\w+(\s+|-)\d{2,4}).*/\1/', -1, term);

          3  pid=prxparse('/\b\d+\W+[a-z]+\W+\d+\b/i');
             do loop and two
             call prxnext(pid,s,e,have,p,l);
             call prxnext(pid,s,e,have,p,l);

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    data have;
    input have $80.;
    cards4;
    Days of 08 April 19
    count on 10 May 2019, 05 May 2018, 08-Jan-2005
    apply i.e. 08 April 19 and 10-Jan-2005
    ;;;;
    run;quit;

    /*
    WORK.HAVE total obs=3

      HAVE

      Days of 08 April 19
      count on 10 May 2019, 05 May 2018, 08-Jan-2005
      apply i.e. 08 April 19 and 10-Jan-2005
    */

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    WORK.WANT total obs=6

    Obs    HAVE                                                 DATE

      Days of 08 April 19                               08 April 19

      count on 10 May 2019, 05 May 2018, 08-Jan-2005    10 May 2019
      count on 10 May 2019, 05 May 2018, 08-Jan-2005    05 May 2018
      count on 10 May 2019, 05 May 2018, 08-Jan-2005    08-Jan-2005

      apply i.e. 08 April 19 and 10-Jan-2005            08 April 19
      apply i.e. 08 April 19 and 10-Jan-2005            10-Jan-2005

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    data want;

     set have;

     do i=1 to countw(have," -");

       * if we get a number then assume it is a day and month and year to follow;
       * should work for dd/mm/yy with added delimiter \;
       if input(scan(have,i," -,"),?? best.) ne . then do;
          date = catx(" ",scan(have,i," "),scan(have,i+1," "),scan(have,i+2," ,"));
          output;
          i=i+2;
       end;
     end;

     drop i;
    run;quit;

