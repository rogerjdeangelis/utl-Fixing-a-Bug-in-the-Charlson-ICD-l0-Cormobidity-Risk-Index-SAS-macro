# utl-Fixing-a-Bug-in-the-Charlson-ICD-l0-Cormobidity-Risk-Index-SAS-macro
Fixing a Bug in the Charlson ICD-10 Cormobidity Risk Index SAS macro
    Fixing a Bug in the Charlson ICD-10 Cormobidity Risk Index SAS macro                                                         
                                                                                                                                 
    The Charson SAS macro has a subtle bug, a missing comma..                                                                    
                                                                                                                                 
    github                                                                                                                       
    https://tinyurl.com/y9qzglt9                                                                                                 
    https://github.com/rogerjdeangelis/utl-Fixing-a-Bug-in-the-Charlson-ICD-l0-Cormobidity-Risk-Index-SAS-macro                  
                                                                                                                                 
    Posted code                                                                                                                  
    https://tinyurl.com/yc868czw                                                                                                 
    http://mchp-appserv.cpe.umanitoba.ca/Upload/SAS/_CharlsonICD10.sas.txt                                                       
                                                                                                                                 
    BUG                                                                                                                          
                                                                                                                                 
    The list of 'CHRONIC PULMONARY DISEASE' diagnosis code has a missing comma                                                   
    between, 'J67''I278', which means that 'I278' is ignored.                                                                    
                                                                                                                                 
     /* Chronic Pulmonary Disease */                                                                                             
     if DX(i) IN: ('J40','J41','J42','J43','J44','J45','J46','J47','J60','J61','J62','J63',                                      
                   'J64','J65','J66','J67''I278','I279','J684','J701','J703')                                                    
                                     ===========                                                                                 
                                     No comma                                                                                    
                                     ===========                                                                                 
                   then CC_GRP_6 = 1;                                                                                            
     LABEL CC_GRP_6 = 'Chronic Pulmonary Disease';                                                                               
                                                                                                                                 
    *_                   _                                                                                                       
    (_)_ __  _ __  _   _| |_                                                                                                     
    | | '_ \| '_ \| | | | __|                                                                                                    
    | | | | | |_) | |_| | |_                                                                                                     
    |_|_| |_| .__/ \__,_|\__|                                                                                                    
            |_|                                                                                                                  
    ;                                                                                                                            
                                                                                                                                 
    * weights for the 17 Charlson categories;                                                                                    
    array wgts[17] wgt1-wgt17 (1 ,1 ,1 ,1 ,1 ,1 ,1 ,1 ,1 ,1 ,2 ,2 ,2 ,2 ,3 ,6 ,6);                                               
                                                                                                                                 
    data have;                                                                                                                   
     informat patid dgn1 dgn2 dgn3 dgn4 dgn5 dgn6 dgn7 dgn8 dgn9 dgn10 $5.;                                                      
     input patid dgn1 dgn2 dgn3 dgn4 dgn5 dgn6 dgn7 dgn8 dgn9 dgn10 $7.;                                                         
    cards4;                                                                                                                      
    A0008 K082 B949 M246 T113 M318 S201 I278 . . .                                                                               
    A0016 P81 M216 F71 T439 V250 N891 E782 . . .                                                                                 
    A0018 T246 V760 Q62 E618 V740 D593 M469 K605 M435 .                                                                          
    A0020 S651 D35 O419 I891 Y472 C185 M351 C060 P714 I250                                                                       
    A0035 T590 S396 Y069 C720 O746 O46 F170 O152 . .                                                                             
    A0038 T235 Q655 M247 V806 M22 F079 C188 . . .                                                                                
    A0042 K750 Q988 V153 R92 I34 V465 B838 O722 G248 .                                                                           
    A0048 V241 I49 O438 N46 T457 L562 Q606 E038 . .                                                                              
    A0051 T842 Y602 H179 T213 I069 F800 D36 T92 . .                                                                              
    A0070 D608 Q435 D528 O753 J06 Q243 E569 . . .                                                                                
    A0074 N009 S925 L731 K860 Y490 R508 V595 Q429 V243 V384                                                                      
    A0090 T869 Q522 T367 V353 C951 U02 V680 Y648 Q228 W74                                                                        
    A0091 F525 R944 G300 V365 P391 Y414 K092 V239 . .                                                                            
    A0093 L701 N140 P22 K560 L579 I99 A25 . . .                                                                                  
    A0102 L531 N990 N840 Y634 P394 N036 V181 N324 . .                                                                            
    A0109 E127 A012 R521 I670 F111 T902 M153 V542 . .                                                                            
    A0110 S640 O901 T252 E070 R293 F068 P526 Y842 . .                                                                            
    A0111 Q453 H043 M131 T214 E071 N901 M257 . . .                                                                               
    A0116 C248 R46 T373 F116 M130 O894 F316 E799 . .                                                                             
    A0119 F981 Y639 V945 E832 A19 S259 V194 . . .                                                                                
    A0120 B358 G959 K090 S334 S19 Y414 D439 D300 J432 X69                                                                        
    A0124 A06 I05 M921 D03 S451 L568 L871 G825 V652 V06                                                                          
    A0130 C380 V818 E42 T141 N490 C961 S489 Y354 F334 .                                                                          
    A0135 R492 Y541 F231 Q12 Q139 D592 G902 . . .                                                                                
    A0140 Y455 T32 L703 N218 V252 M30 D120 . . .                                                                                 
    A0143 R63 L893 L293 H93 O047 S550 N42 N06 K068 .                                                                             
    A0151 B330 D33 R638 K718 C944 S244 P015 Q26 . .                                                                              
    A0157 E724 P360 H690 H720 A413 Y495 F650 . . .                                                                               
    A0158 V941 D690 B718 M84 P969 T06 F184 S931 G258 M224                                                                        
    A0164 X12 Y588 Q922 F51 E649 A50 E308 . . .                                                                                  
    ;;;;                                                                                                                         
    run;quit;                                                                                                                    
                                                                                                                                 
                                                                                                                                 
    WORK.HAVE total obs=30                                                                                                       
                                                                                                                                 
      PATID    DGN1    DGN2    DGN3    DGN4    DGN5    DGN6    DGN7    DGN8    DGN9    DGN10                                     
                                                                                                                                 
      A0008    K082    B949    M246    T113    M318    S201    I278                                                              
      A0016    P81     M216    F71     T439    V250    N891    E782                                                              
      A0018    T246    V760    Q62     E618    V740    D593    M469    K605    M435                                              
      A0020    S651    D35     O419    I891    Y472    C185    M351    C060    P714    I250                                      
      A0035    T590    S396    Y069    C720    O746    O46     F170    O152                                                      
      A0038    T235    Q655    M247    V806    M22     F079    C188                                                              
      A0042    K750    Q988    V153    R92     I34     V465    B838    O722    G248                                              
      A0048    V241    I49     O438    N46     T457    L562    Q606    E038                                                      
      A0051    T842    Y602    H179    T213    I069    F800    D36     T92                                                       
    ....                                                                                                                         
                                                                                                                                 
    *            _               _                                                                                               
      ___  _   _| |_ _ __  _   _| |_                                                                                             
     / _ \| | | | __| '_ \| | | | __|                                                                                            
    | (_) | |_| | |_| |_) | |_| | |_                                                                                             
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                            
                    |_|                                                                                                          
    ;                                                                                                                            
                                                                                                                                 
    WORK.WANT total obs=30                                                                                                       
                                                                                                                                 
                                                                                                                                 
               UNWEIGHTED     WEIGHTED                                                                                           
      PATID    TOT_GRP        TOT_WGT                                                                                            
                                                                                                                                 
      A0008       1              1                                                                                               
      A0016       0              0                                                                                               
      A0018       0              0                                                                                               
                                                                                                                                 
      A0020       2              3   Weighted is always greater than or equal to unweighted                                      
                                                                                                                                 
      A0035       1              2                                                                                               
      A0038       1              2                                                                                               
      A0042       0              0                                                                                               
      A0048       0              0                                                                                               
      A0051       0              0                                                                                               
      A0070       0              0                                                                                               
    ...                                                                                                                          
                                                                                                                                 
    *          _       _   _                                                                                                     
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                          
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                         
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                        
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                        
                                                                                                                                 
    ;                                                                                                                            
                                                                                                                                 
    %macro utl_CharlsonICD10 (                                                                                                   
                 DATA =  /* input data set */                                                                                    
                ,OUT  =  /* output data set */                                                                                   
                ,id   =  /* patient id */                                                                                        
                ,dX   =  /* dgns_cd1-dgns_cd25 */                                                                                
           );                                                                                                                    
                                                                                                                                 
          data &OUT;                                                                                                             
                                                                                                                                 
          retain &id;                                                                                                            
          retain tot_grp tot_wgt 0;                                                                                              
                                                                                                                                 
          set &DATA ;                                                                                                            
                                                                                                                                 
          tot_wgt = 0;                                                                                                           
                                                                                                                                 
          /*  set up array for individual CCI group counters */                                                                  
          array CC_GRP (17) CC_GRP_1 - CC_GRP_17;                                                                                
                                                                                                                                 
          /*  set up array for 25 diagnosis codes within a record  */                                                            
          array DX (*) &dx;                                                                                                      
                                                                                                                                 
          /* Weights for weighted score */                                                                                       
          array wgts[17] wgt1-wgt17 (1 ,1 ,1 ,1 ,1 ,1 ,1 ,1 ,1 ,1 ,2 ,2 ,2 ,2 ,3 ,6 ,6);                                         
                                                                                                                                 
                                                                                                                                 
          /*  initialize all CCI group counters to zero */                                                                       
          do i = 1 to 17;                                                                                                        
             CC_GRP(i) = 0;                                                                                                      
          end;                                                                                                                   
                                                                                                                                 
          /*  check each patient record for the diagnosis codes in each CCI group */                                             
          do i = 1 to dim(dx) UNTIL (DX(i)=' ');     /* for each set of diagnoses codes */                                       
                                                                                                                                 
               /* Myocardial Infarction */                                                                                       
               if DX(i) IN: ('I21', 'I22','I252') then CC_GRP_1 = 1;                                                             
               LABEL CC_GRP_1 = 'Myocardial Infarction';                                                                         
                                                                                                                                 
               /* Congestive Heart Failure */                                                                                    
               if DX(i) IN: ('I43','I50','I099','I110','I130','I132','I255','I420','I425','I426',                                
                             'I427','I428','I429','P290') then CC_GRP_2 = 1;                                                     
               LABEL CC_GRP_2 = 'Congestive Heart Failure';                                                                      
                                                                                                                                 
               /* Periphral Vascular Disease */                                                                                  
               if DX(i) IN: ('I70','I71','I731','I738','I739','I771','I790','I792','K551','K558',                                
                             'K559','Z958','Z959') then CC_GRP_3 = 1;                                                            
               LABEL CC_GRP_3 = 'Periphral Vascular Disease';                                                                    
                                                                                                                                 
               /* Cerebrovascular Disease */                                                                                     
               if DX(i) IN: ('G45','G46','I60','I61','I62','I63','I64','I65','I66','I67','I68',                                  
                             'I69','H340') then CC_GRP_4 = 1;                                                                    
               LABEL CC_GRP_4 = 'Cerebrovascular Disease';                                                                       
                                                                                                                                 
               /* Dementia */                                                                                                    
               if DX(i) IN: ('F00','F01','F02','F03','G30','F051','G311')                                                        
                             then CC_GRP_5 = 1;                                                                                  
               LABEL CC_GRP_5 = 'Dementia';                                                                                      
                                                                                                                                 
               /* Chronic Pulmonary Disease */                                                                                   
               if DX(i) IN: ('J40','J41','J42','J43','J44','J45','J46','J47','J60','J61','J62','J63',                            
                             'J64','J65','J66','J67','I278','I279','J684','J701','J703')                                         
                             then CC_GRP_6 = 1;                                                                                  
               LABEL CC_GRP_6 = 'Chronic Pulmonary Disease';                                                                     
                                                                                                                                 
               /* Connective Tissue Disease-Rheumatic Disease */                                                                 
               if DX(i) IN: ('M05','M32','M33','M34','M06','M315','M351','M353','M360')                                          
                             then CC_GRP_7 = 1;                                                                                  
               LABEL CC_GRP_7 = 'Connective Tissue Disease-Rheumatic Disease';                                                   
                                                                                                                                 
               /* Peptic Ulcer Disease */                                                                                        
               if DX(i) IN: ('K25','K26','K27','K28') then CC_GRP_8 = 1;                                                         
               LABEL CC_GRP_8 = 'Peptic Ulcer Disease';                                                                          
                                                                                                                                 
               /* Mild Liver Disease */                                                                                          
               if DX(i) IN: ('B18','K73','K74','K700','K701','K702','K703','K709','K717','K713',                                 
                             'K714','K715','K760','K762','K763','K764','K768','K769','Z944')                                     
                             then CC_GRP_9 = 1;                                                                                  
               LABEL CC_GRP_9 = 'Mild Liver Disease';                                                                            
                                                                                                                                 
               /* Diabetes without complications */                                                                              
               if DX(i) IN: ('E100','E101','E106','E108','E109','E110','E111','E116','E118','E119',                              
                             'E120','E121','E126','E128','E129','E130','E131','E136','E138','E139',                              
                             'E140','E141','E146','E148','E149') then CC_GRP_10 = 1;                                             
               LABEL CC_GRP_10 = 'Diabetes without complications';                                                               
                                                                                                                                 
               /* Diabetes with complications */                                                                                 
               if DX(i) IN: ('E102','E103','E104','E105','E107','E112','E113','E114','E115','E117',                              
                             'E122','E123','E124','E125','E127','E132','E133','E134','E135','E137',                              
                             'E142','E143','E144','E145','E147') then CC_GRP_11 = 1;                                             
               LABEL CC_GRP_11 = 'Diabetes with complications';                                                                  
                                                                                                                                 
               /* Paraplegia and Hemiplegia */                                                                                   
               if DX(i) IN: ('G81','G82','G041','G114','G801','G802','G830','G831','G832','G833',                                
                             'G834','G839') then CC_GRP_12 = 1;                                                                  
               LABEL CC_GRP_12 = 'Paraplegia and Hemiplegia';                                                                    
                                                                                                                                 
               /* Renal Disease */                                                                                               
               if DX(i) IN: ('N18','N19','N052','N053','N054','N055','N056','N057','N250','I120',                                
                             'I131','N032','N033','N034','N035','N036','N037','Z490','Z491','Z492',                              
                             'Z940','Z992') then CC_GRP_13 = 1;                                                                  
               LABEL CC_GRP_13 = 'Renal Disease';                                                                                
                                                                                                                                 
               /* Cancer */                                                                                                      
               if DX(i) IN: ('C00','C01','C02','C03','C04','C05','C06','C07','C08','C09','C10','C11',                            
                             'C12','C13','C14','C15','C16','C17','C18','C19','C20','C21','C22','C23',                            
                             'C24','C25','C26','C30','C31','C32','C33','C34','C37','C38','C39','C40',                            
                             'C41','C43','C45','C46','C47','C48','C49','C50','C51','C52','C53','C54',                            
                             'C55','C56','C57','C58','C60','C61','C62','C63','C64','C65','C66','C67',                            
                             'C68','C69','C70','C71','C72','C73','C74','C75','C76','C81','C82','C83',                            
                             'C84','C85','C88','C90','C91','C92','C93','C94','C95','C96','C97')                                  
                             then CC_GRP_14 = 1;                                                                                 
               LABEL CC_GRP_14 = 'Cancer';                                                                                       
                                                                                                                                 
               /* Moderate or Severe Liver Disease */                                                                            
               if DX(i) IN: ('K704','K711','K721','K729','K765','K766','K767','I850','I859','I864','I982')                       
                             then CC_GRP_15 = 1;                                                                                 
               LABEL CC_GRP_15 = 'Moderate or Severe Liver Disease';                                                             
                                                                                                                                 
               /* Metastatic Carcinoma */                                                                                        
               if DX(i) IN: ('C77','C78','C79','C80') then CC_GRP_16 = 1;                                                        
               LABEL CC_GRP_16 = 'Metastatic Carcinoma';                                                                         
                                                                                                                                 
               /* AIDS/HIV */                                                                                                    
               if DX(i) IN: ('B20','B21','B22','B24') then CC_GRP_17 = 1;                                                        
               LABEL CC_GRP_17 = 'AIDS/HIV';                                                                                     
                                                                                                                                 
          end;                   /* end do i = 1 to 25 */                                                                        
                                                                                                                                 
          /* Count total number of groups for each record */                                                                     
                                                                                                                                 
         TOT_GRP = CC_GRP_1  + CC_GRP_2  + CC_GRP_3  + CC_GRP_4  + CC_GRP_5  + CC_GRP_6  + CC_GRP_7  + CC_GRP_8  +               
                   CC_GRP_9  + CC_GRP_10 + CC_GRP_11 + CC_GRP_12 + CC_GRP_13 + CC_GRP_14 + CC_GRP_15 + CC_GRP_16 +               
                   CC_GRP_17;                                                                                                    
                                                                                                                                 
          do ix=1 to 17;                                                                                                         
             tot_wgt = tot_wgt + CC_GRP[ix]*wgts[ix];                                                                            
             keep &id tot_grp tot_wgt;                                                                                           
          end;                                                                                                                   
                                                                                                                                 
          LABEL TOT_GRP = 'CCI Group Score';                                                                                     
          LABEL TOT_wgt = 'Weighted CCI Groups Score';                                                                           
                                                                                                                                 
          run;                                                                                                                   
                                                                                                                                 
          options notes ;                                                                                                        
           %put ;                                                                                                                
           %put NOTE: utl_Charlson Finished &out created ;                                                                       
         %put ;                                                                                                                  
                                                                                                                                 
                                                                                                                                 
    %mend utl_CharlsonICD10;                                                                                                     
                                                                                                                                 
    %utl_CharlsonICD10 (                                                                                                         
                 DATA =  have                                                                                                    
                ,OUT  =  want                                                                                                    
                ,id   =  patid                                                                                                   
                ,dX   =  dgn1-dgn10                                                                                              
           );                                                                                                                    
                                                                                                                                 
                                                                                                                                 
