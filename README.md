# utl-create-mutiple-pdf-files-from-one-table-dosubl-ods-newfile-option
Create mutiple pdf files from one table dosubl ods newfile option 
    %let pgm=utl-create-mutiple-pdf-files-from-one-table-dosubl-ods-newfile-option;

    Create mutiple pdf files from one table dosubl ods newfile option

    Two Solutions

        1 ods bygroup
        2 ods dosubl

     Relsated repos on end

    github
    http://tinyurl.com/4kecbfk8
    https://github.com/rogerjdeangelis/utl-create-mutiple-pdf-files-from-one-table-dosubl-ods-newfile-option

    see
    https://goo.gl/fKttVq
    https://communities.sas.com/t5/General-SAS-Programming/How-to-Export-your-SAS-as-pdf/m-p/370635

    Cynthia_sas
    https://communities.sas.com/t5/user/viewprofilepage/user-id/13549

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                    |                                                 |                                                 */
    /*             INPUT  |                                                 |             d:\pdf\bygrp_age1.pdf               */
    /*                    |  PROCESS                                        |             =====================               */
    /*                    |                                                 |                                                 */
    /*   NAME    SEX AGE  |  SAS BYGROUP                                    |             AGE=12                              */
    /*                    |                                                 |                                                 */
    /*   James    M   12  |  ods pdf file="d:\pdf\bygrp_age1.pdf"           |             AGE     NAME     SEX                */
    /*   Jane     F   12  |    newfile=bygroup;                             |                                                 */
    /*   John     M   12  |  proc print data=class;                         |              12    James      M                 */
    /*   Louise   F   12  |  by age;                                        |              12    Jane       F                 */
    /*   Robert   M   12  |                                                 |              12    John       M                 */
    /*   Alice    F   13  |  SAS BYGROUP (DOSUBL)                           |              12    Louise     F                 */
    /*   Barbara  F   13  | =====================                           |              12    Robert     M                 */
    /*   Jeffrey  M   13  |  set class;                                     |                                                 */
    /*   Alfred   M   14  |  by age;                                        |                                                 */
    /*   Carol    F   14  |  if first.age then do;                          |             d:\pdf\bygrp_age2.pdf               */
    /*   Henry    M   14  |    call symputx('age',age);                     |             =====================               */
    /*   Judy     F   14  |    rc=dosubl('                                  |                                                 */
    /*                    |      ods pdf file="d:\pdf\bygrp_age&age..pdf";  |             AGE=13                              */
    /*                    |       proc print data=class(where=(age=&age));  |                                                 */
    /*                    |           var age name sex height weight;       |             AGE     NAME      SEX               */
    /*                    |        run;                                     |                                                 */
    /*                    |      ods pdf close;                             |              13    Alice       F                */
    /*                    |     ');                                         |              13    Barbara     F                */
    /*                    |                                                 |              13    Jeffrey     M                */
    /*                    |                                                 |                                                 */
    /*                    |                                                 |                                                 */
    /*                    |                                                 |             d:\pdf\bygrp_age3.pdf               */
    /*                    |                                                 |             =====================               */
    /*                    |                                                 |                                                 */
    /*                    |                                                 |             AGE=14                              */
    /*                    |                                                 |                                                 */
    /*                    |                                                 |             AGE     NAME     SEX                */
    /*                    |                                                 |                                                 */
    /*                    |                                                 |              14    Alfred     M                 */
    /*                    |                                                 |              14    Carol      F                 */
    /*                    |                                                 |              14    Henry      M                 */
    /*                    |                                                 |              14    Judy       F                 */
    /*                    |                                                 |                                                 */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    proc sort data=sashelp.class(keep=name age sex)
        out=class;
      by age;
      where age in (12, 13, 14) ;
    run;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Obs    NAME       SEX    AGE                                                                                          */
    /*                                                                                                                        */
    /*    1    James       M      12                                                                                          */
    /*    2    Jane        F      12                                                                                          */
    /*    3    John        M      12                                                                                          */
    /*    4    Louise      F      12                                                                                          */
    /*    5    Robert      M      12                                                                                          */
    /*    6    Alice       F      13                                                                                          */
    /*    7    Barbara     F      13                                                                                          */
    /*    8    Jeffrey     M      13                                                                                          */
    /*    9    Alfred      M      14                                                                                          */
    /*   10    Carol       F      14                                                                                          */
    /*   11    Henry       M      14                                                                                          */
    /*   12    Judy        F      14                                                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*             _       _
    / |   ___   __| |___  | |__  _   _  __ _ _ __ ___  _   _ _ __
    | |  / _ \ / _` / __| | `_ \| | | |/ _` | `__/ _ \| | | | `_ \
    | | | (_) | (_| \__ \ | |_) | |_| | (_| | | | (_) | |_| | |_) |
    |_|  \___/ \__,_|___/ |_.__/ \__, |\__, |_|  \___/ \__,_| .__/
                                 |___/ |___/                |_|
    */

    ods pdf file="d:\pdf\bygrp_age1.pdf" newfile=bygroup;
      proc print data=class;
        by age;
        var age name sex height weight;
      run;
    ods pdf close;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*     d:\pdf\bygrp_age1.pdf     d:\pdf\bygrp_age2.pdf     d:\pdf\bygrp_age3.pdf                                          */
    /*     =====================     =====================     =====================                                          */
    /*                                                                                                                        */
    /*     AGE=12                    AGE=13                    AGE=14                                                         */
    /*                                                                                                                        */
    /*     AGE     NAME     SEX      AGE     NAME      SEX     AGE     NAME     SEX                                           */
    /*                                                                                                                        */
    /*      12    James      M        13    Alice       F       14    Alfred     M                                            */
    /*      12    Jane       F        13    Barbara     F       14    Carol      F                                            */
    /*      12    John       M        13    Jeffrey     M       14    Henry      M                                            */
    /*      12    Louise     F                                  14    Judy       F                                            */
    /*      12    Robert     M                                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/
    /*___              _           _                 _     _
    |___ \    ___   __| |___    __| | ___  ___ _   _| |__ | |
      __) |  / _ \ / _` / __|  / _` |/ _ \/ __| | | | `_ \| |
     / __/  | (_) | (_| \__ \ | (_| | (_) \__ \ |_| | |_) | |
    |_____|  \___/ \__,_|___/  \__,_|\___/|___/\__,_|_.__/|_|

    */

    %symdel age;
    data _null_;

       set class;
       by age;
       if first.age then do;
         call symputx('age',age);
         rc=dosubl('
           ods pdf file="d:\pdf\bygrp_age_&age..pdf";
             proc print data=class(where=(age=&age));
                title "Age=&age";
                var age name sex ;
             run;
           ods pdf close;
          ');

       end;

    run;quit;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*     d:\pdf\bygrp_age_12.pdf   d:\pdf\bygrp_age13.pdf    d:\pdf\bygrp_age_14.pdf                                        */
    /*     =====================     =====================     =====================                                          */
    /*                                                                                                                        */
    /*     AGE=12                    AGE=13                    AGE=14                                                         */
    /*                                                                                                                        */
    /*     AGE     NAME     SEX      AGE     NAME      SEX     AGE     NAME     SEX                                           */
    /*                                                                                                                        */
    /*      12    James      M        13    Alice       F       14    Alfred     M                                            */
    /*      12    Jane       F        13    Barbara     F       14    Carol      F                                            */
    /*      12    John       M        13    Jeffrey     M       14    Henry      M                                            */
    /*      12    Louise     F                                  14    Judy       F                                            */
    /*      12    Robert     M                                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*        _       _           _
     _ __ ___| | __ _| |_ ___  __| |  _ __ ___ _ __   ___  ___
    | `__/ _ \ |/ _` | __/ _ \/ _` | | `__/ _ \ `_ \ / _ \/ __|
    | | |  __/ | (_| | ||  __/ (_| | | | |  __/ |_) | (_) \__ \
    |_|  \___|_|\__,_|\__\___|\__,_| |_|  \___| .__/ \___/|___/
                                              |_|
    */

    REPO
    ------------------------------------------------------------------------------------------------------------------------------------
    https://github.com/rogerjdeangelis/utl-convert-pdf-to-text-using-python-and-r
    https://github.com/rogerjdeangelis/utl-create-a-simple-n-percent-clinical-table-in-r-sas-wps-python-output-pdf-rtf-xlsx-html-list
    https://github.com/rogerjdeangelis/utl-creating-identical-pdf-and-powerpoint-slides
    https://github.com/rogerjdeangelis/utl-identical-side-by-side-text-and-graphics-in-pdf-and-powerpoint
    https://github.com/rogerjdeangelis/utl-overlaying-histograms-and-scatterplots-in-powerpoint-pdf-and-jpeg
    https://github.com/rogerjdeangelis/utl-putting-a-frame-around-text-in-doc-rtf-and-pdf-ods-destinations-with-and-without-layout
    https://github.com/rogerjdeangelis/utl-removing-unwanted-bookmarks-in-pdf-table-of-contents-toc
    https://github.com/rogerjdeangelis/utl-scraping-pdf-output-for-pdf-tables-and-lists
    https://github.com/rogerjdeangelis/utl-side-by-side-proc-report-output-in-pdf-html-and-excel
    https://github.com/rogerjdeangelis/utl_combine_pdf_files_and_delete_pages_from_a_pdf_pyPDF_ghostscript
    https://github.com/rogerjdeangelis/utl_combining_all_pdf_files_in_a_directory
    https://github.com/rogerjdeangelis/utl_convert_pdf_tables_to_SAS_WPS_datasets
    https://github.com/rogerjdeangelis/utl_convert_pdf_tables_to_sas_tables
    https://github.com/rogerjdeangelis/utl_dropping-down-to-R-and-converting-pdfs-to-sas-tables-and-text
    https://github.com/rogerjdeangelis/utl_dropping-down-to-powershell-and-converting-doc-and-rtf-files-to-pdfs
    https://github.com/rogerjdeangelis/utl_ods_pdf_and_rtf_two_different_page_titles_on_the_same_page
    https://github.com/rogerjdeangelis/utl_pdf_graphics_top_40_a_sas_ods_graphics_look_at_chicago_public_schools_salaries_by_job
    https://github.com/rogerjdeangelis/utl_report_does_not_show_group_variable_across_new_pages_in_rtf_and_pdf

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
