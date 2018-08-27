# utl_surpressing_input_and_output_warnings_when_variables_are_missing
Surpressing input and output warnings when variables are missing.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Surpressing input and output warnings when variables are missing

    options dkricond=nowarn dkrocond=nowarn;
    First one is for input datasets, second one is for output datasets.

    File this in your synapses for future reference

    github
    https://tinyurl.com/y9u73j6y
    https://github.com/rogerjdeangelis/utl_surpressing_input_and_output_warnings_when_variables_are_missing

    see
    https://tinyurl.com/y7v4rxmg
    https://stackoverflow.com/questions/51974144/how-do-i-get-sas-to-ignore-missing-variable-names

    Orh profile
    https://stackoverflow.com/users/675727/orh


    When to use
       dkricond=nowarn dkrocond=nowarn


    INPUT WARNINGS
    =============

     PROBLEM: Need to eliminate warnings on missing input variables
     --------------------------------------------------------------

       data class;
         set sashelp.class(drop=varNot keep=varMis rename=varNam=Nam);
       run;quit;

       1049     data class;
       1050       set sashelp.class(drop=varNot keep=varMis rename=varName=name);

       WARNING: Variable VARNAM is not on file SASHELP.CLASS.
       WARNING: The variable VARNOT in the DROP, KEEP, or RENAME list has never been referenced.  DROP
       WARNING: The variable VARMIS in the DROP, KEEP, or RENAME list has never been referenced.  KEEP
       WARNING: The variable VARNAM in the DROP, KEEP, or RENAME list has never been referenced.  RENAME

       1051     run;

       NOTE: There were 19 observations read from the data set SASHELP.CLASS.

     SOLUTION:
     ---------

       options dkricond=nowarn;
       data class;
          set sashelp.class(drop=varNot keep=varMis rename=varName=name);
       run;quit;
       options dkricond=warn;

       1052    options dkricond=nowarn;
       1053     data class;
       1054       set sashelp.class(drop=varNot rename=varName=name);
       1055     run;

       NOTE: There were 19 observations read from the data set SASHELP.CLASS.


    OUTPUT WARNINGS
    ==============

     PROBLEM: Need to eliminate output warnings on missing output variables
     ----------------------------------------------------------------------

      data class(drop=varMis keep=varNot rename=varName=name);
        set sashelp.class;
      run;

       1049     data class;
       1050       set sashelp.class(drop=varMis keep=varNot rename=varName=name);

       WARNING: The variable VARMIS in the DROP, KEEP, or RENAME list has never been referenced.
       WARNING: The variable VARNOT in the DROP, KEEP, or RENAME list has never been referenced.
       WARNING: The variable VARNAME in the DROP, KEEP, or RENAME list has never been referenced.

       1051     run;

       NOTE: There were 19 observations read from the data set SASHELP.CLASS.

     SOLUTION:
     --------

       options dkrocond=nowarn;
       data class(drop=varMis keep=varNot rename=varName=name);
         set sashelp.class;;
       run;quit;
       options dkricond=warn;

       1052    options dkricond=nowarn;
       1053     data class(drop=varMis keep=varNot rename=varName=name);;
       1054       set sashelp.class;
       1055     run;

       NOTE: There were 19 observations read from the data set SASHELP.CLASS.


    INPUT and OUTPUTS
    ================

     PROBLEM: Need to eliminate input and output warnings on missing output variables

      data class(drop=varMis keep=varNot rename=varName=name);
        set sashelp.class(drop=varAny keep=varOne rename=varRen=name);;
      run;

      1151   data class(drop=varMis keep=varNot rename=varName=name);
      1152      set sashelp.class(drop=varAny keep=varOne rename=varRen=name);

      WARNING: Variable VARREN is not on file SASHELP.CLASS.
      WARNING: The variable VARANY in the DROP, KEEP, or RENAME list has never been referenced.
      WARNING: The variable VARONE in the DROP, KEEP, or RENAME list has never been referenced.
      WARNING: The variable VARREN in the DROP, KEEP, or RENAME list has never been referenced.
      1153    run;

      WARNING: The variable VARMIS in the DROP, KEEP, or RENAME list has never been referenced.
      WARNING: The variable VARNOT in the DROP, KEEP, or RENAME list has never been referenced.
      WARNING: The variable VARNAME in the DROP, KEEP, or RENAME list has never been referenced.

     SOLUTION
     --------
      options dkricond=nowarn dkrocond=nowarn;
      data class(drop=varMis keep=varNot rename=varName=name);
        set sashelp.class(drop=varAny keep=varOne rename=varRen=name);;
      run;
      options dkricond=warn dkrocond=warn;

       NOTE: There were 19 observations read from the data set SASHELP.CLASS.


