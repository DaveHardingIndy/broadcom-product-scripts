# Dynamic Environment Cleanup

These utilities support an Endevor Dynamic Environment Cleanup Process

These samples are provided as is and are not officially supported (see [license](https://github.com/BroadcomMFD/broadcom-product-scripts/blob/main/LICENSE
) for more information).

Important notes:
1) This process uses 'DYNENV' as the Type name for Dynamic Environments.
   DYNENV is hard-coded in several locations. If you change it, find
   and replace all occurrences.
2) This process uses 'DEV' as the Environment where Type DYNENV is
   defined / allowed. There are hard-code references for DEV as well
   as DEV1 (DEV stage 1) and DEV2 (DEV stage 2). Update these for
   your site.
3) Dataset naming conventions are critical. You must have a way
   to uniquely identify DYNENV datasets so this means the Environment
   name MUST be a node in the datasets. For example:
     'NDV.&C1EN..&C1SU..&C1EN(1,1)&C1S#..LOADLIB'

**Description & Notes**

**CLEANDYN**  Batch job that drives the cleanup process. Most of your
          site specific customizations will be done here.

          1) The WARN=XX value is the number of days (without activity)
             before sending out the 'warning email' for DYNENVs which
             are nearing the purge / cleanup date.
          2) The PURGE=XX value is the number of days (without activity)
             before archiving inactive DYNENVs elements and deleting
             all DYNENV definitions & datasets.
          3) Review all steps but for JSTEP10, replace the list of
             environments with what's defined in your C1DEFTLS table.
          4) There is an email step in this job. To use, SMTP or
             CSSMTP must be enabled at your site. Also, there is a
             hard-coded '55 days' in the email. Update to match the
             PURGE=XX value.

**DDYNENV**   Sample Delete Processor for Dynamic Environments.

**ESMTPTBL**  Sample ESMTPTBL (for reference only). This process
          assumes your version of this table is saved to a PDS/PDSE.
          It is then referenced by job CLEANDYN so emails can be
          included in the 'about to be purged' report.

**GDYNENV** Sample Generate Processor for Dynamic Environments. This
          also contains the list of prerequisites for Dynamic
          Environments.

**RCSVLIST**  Rexx- build CSV List Element SCL.

**RDYNCHK**   Rexx- Find empty DYNENVs and create DELETE SCL.

**RJULIAN**   Rexx- Convert YYYYMMDD dates (from Endevor) to Julian format.

**RPURGE2**   Rexx- Build ARCHIVE SCL for DYNENV purge process.

**RUNUSED2**  Rexx- Find DYNENVs with no activity for XX days.

