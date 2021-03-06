# irs-990-statistics-of-income-extracts

R scripts and documentation used to read the IRS Statistics of Income extracts.



## SOI Tax Stats - Annual Extract of Tax-Exempt Organization Financial Data - 2012-2015

https://www.irs.gov/uac/soi-tax-stats-annual-extract-of-tax-exempt-organization-financial-data

 
"These extracts contain selected financial data from filers of three Internal Revenue Service (IRS) information returns — Forms 990, 990-EZ and 990-PF — collected for program administrative purposes. During IRS administrative processing, some adjustments are made which can result in differences between the information as originally reported and the data on this extract. Other differences may be introduced during transcription of paper-filed return information. Prior to release, we also review and make additional adjustments to the data to ensure their fitness for analytical and statistical purposes."

These SOI files contain the EIN as unique identifiers, but they do not contain information from the 990 header like the organizational name, location, or NTEE. As a result, to be useful you may need to merge these files with the IRS Master Business File or NCCS Master Business Files.


## LOAD 2015 FILES

"The extracts are in a space-delimited, ASCII format."

Here is an example of how to download and process the ASCII files in R.



```r


# 2015 Form 990 data

dat1 <- read.csv( "https://www.irs.gov/pub/irs-soi/15eofinextract990.dat.dat", sep=" ", skip=1 )

raw.names <- readLines( "https://www.irs.gov/pub/irs-soi/15eofinextract990.dat.dat", n=1 )

dat.names <- strsplit( raw.names, " ")[[1]]

names( dat1 ) <- dat.names

head( dat1 )

write.csv( dat1, "2015-Form-990-PC-SOI.csv", row.names=F )





# 2015 Form 990-EZ data

dat2 <- read.csv( "https://www.irs.gov/pub/irs-soi/15eofinextractEZ.dat", sep=" ", skip=1 )

raw.names <- readLines( "https://www.irs.gov/pub/irs-soi/15eofinextractEZ.dat", n=1 )

dat.names <- strsplit( raw.names, " ")[[1]]

names( dat2 ) <- dat.names

head( dat2 )

write.csv( dat2, "2015-Form-990-EZ-SOI.csv", row.names=F )


```





## LINKS TO DATA

**2015**

https://www.irs.gov/pub/irs-soi/15eofinextractEZ.dat

https://www.irs.gov/pub/irs-soi/15eofinextract990.dat.dat


**2014**

https://www.irs.gov/pub/irs-soi/14eofinextract990.zip

https://www.irs.gov/pub/irs-soi/14eofinextract990ez.zip


**2013**

https://www.irs.gov/pub/irs-soi/13eofinextract990.zip

https://www.irs.gov/pub/irs-soi/13eofinextract990ez.zip

**2012**

https://www.irs.gov/pub/irs-soi/12eofinextract990.zip

https://www.irs.gov/pub/irs-soi/12eofinextract990ez.zip



**Data Dictionaries**

https://www.irs.gov/pub/irs-soi/15eofinextractdoc.xls

https://www.irs.gov/pub/irs-soi/14eofinextractdoc.xls

https://www.irs.gov/pub/irs-soi/13eofinextractdoc.xls

https://www.irs.gov/pub/irs-soi/12eofinextractdoc.xls








## 2015 990 DATA DICTIONARY

ELEMENT NAME	|	DESCRIPTION	|	LOCATION	|	TYPE	|	LENGTH
----------------|-----------------------|-----------------------|---------------|--------------------------------
elf	|	E-file indicator	|	n/a	|	Char	|	1
EIN	|	Employer Identification Number	|	Form 990 Header	|	Num	|	9
tax_pd	|	Tax period	|	Form 990 Header	|	Num	|	6
subseccd	|	Subsection code	|	Form 990 Header	|	Num	|	2
s501c3or4947a1cd	|	Described in 501(c)(3)?	|	990 Core_Pt IV-1	|	Char	|	1
schdbind	|	Schedule B required?	|	990 Core_Pt IV-2	|	Char	|	1
politicalactvtscd	|	Political activities?	|	990 Core_Pt IV-3	|	Char	|	1
lbbyingactvtscd	|	Lobbying activities?	|	990 Core_Pt IV-4	|	Char	|	1
subjto6033cd	|	Subject to proxy tax?	|	990 Core_Pt IV-5	|	Char	|	1
dnradvisedfundscd	|	Donor advised funds?	|	990 Core_Pt IV-6	|	Char	|	1
prptyintrcvdcd	|	Conservation easements?	|	990 Core_Pt IV-7	|	Char	|	1
maintwrkofartcd	|	Collections of art?	|	990 Core_Pt IV-8	|	Char	|	1
crcounselingqstncd	|	Credit counseling?	|	990 Core_Pt IV-9	|	Char	|	1
hldassetsintermpermcd	|	Term or permanent endowments?	|	990 Core_Pt IV-10	|	Char	|	1
rptlndbldgeqptcd	|	Land buildings and equipment reported?	|	990 Core_Pt IV-11a	|	Char	|	1
rptinvstothsecd	|	Investments in other securities reported?	|	990 Core_Pt IV-11b	|	Char	|	1
rptinvstprgrelcd	|	Program related investments reported?	|	990 Core_Pt IV-11c	|	Char	|	1
rptothasstcd	|	Other assets reported?	|	990 Core_Pt IV-11d	|	Char	|	1
rptothliabcd	|	Other liabilities reported?	|	990 Core_Pt IV-11e	|	Char	|	1
sepcnsldtfinstmtcd	|	Separate consolidated financial statement	|	990 Core_Pt IV - 11f	|	Char	|	1
sepindaudfinstmtcd	|	Separate audited financial statement	|	990 Core_Pt IV - 12a	|	Char	|	1
inclinfinstmtcd	|	Included in consolidated financial statements?	|	990 Core_Pt IV - 12b	|	Char	|	1
operateschools170cd	|	School?	|	990 Core_Pt IV-13	|	Char	|	1
frgnofficecd	|	Foreign office?	|	990 Core_Pt IV-14a	|	Char	|	1
frgnrevexpnscd	|	Foreign activities, etc?	|	990 Core_Pt IV-14b	|	Char	|	1
frgngrntscd	|	More than $5000 to organizations Part IX, line 3?	|	990 Core_Pt IV-15	|	Char	|	1
frgnaggragrntscd	|	More than $5000 to individuals Part IX, line 3?	|	990 Core_Pt IV-16	|	Char	|	1
rptprofndrsngfeescd	|	Professional fundraising?	|	990 Core_Pt IV-17	|	Char	|	1
rptincfnndrsngcd	|	Fundraising activities?	|	990 Core_Pt IV-18	|	Char	|	1
rptincgamingcd	|	Gaming?	|	990 Core_Pt IV-19	|	Char	|	1
operatehosptlcd	|	Hospital?	|	990 Core_Pt IV-20a	|	Char	|	1
hospaudfinstmtcd	|	Hospital audited financial statement included?	|	990 Core_Pt IV - 20b	|	Char	|	1
rptgrntstogovtcd	|	Grants to organizations?	|	990 Core_Pt IV-21	|	Char	|	1
rptgrntstoindvcd	|	Grants to individuals?	|	990 Core_Pt IV-22	|	Char	|	1
rptyestocompnstncd	|	Schedule J required?	|	990 Core_Pt IV-23	|	Char	|	1
txexmptbndcd	|	Tax exempt bonds?	|	990 Core_Pt IV-24a	|	Char	|	1
invstproceedscd	|	Investment income?	|	990 Core_Pt IV-24b	|	Char	|	1
maintescrwaccntcd	|	Escrow account?	|	990 Core_Pt IV-24c	|	Char	|	1
actonbehalfcd	|	On behalf of issuer?	|	990 Core_Pt IV-24d	|	Char	|	1
engageexcessbnftcd	|	Excess benefit transaction?	|	990 Core_Pt IV-25a	|	Char	|	1
awarexcessbnftcd	|	Prior excess benefit transaction?	|	990 Core_Pt IV-25b	|	Char	|	1
loantofficercd	|	Loan to officer or DQP?	|	990 Core_Pt IV-26	|	Char	|	1
grantoofficercd	|	Grant to related person?	|	990 Core_Pt IV-27	|	Char	|	1
dirbusnreltdcd	|	Business relationship with organization?	|	990 Core_Pt IV-28a	|	Char	|	1
fmlybusnreltdcd	|	Business relationship thru family member?	|	990 Core_Pt IV-28b	|	Char	|	1
servasofficercd	|	Officer, etc. of entity with business relationship?	|	990 Core_Pt IV-28c	|	Char	|	1
recvnoncashcd	|	Deductible non-cash contributions?	|	990 Core_Pt IV-29	|	Char	|	1
recvartcd	|	Deductible contributions of art, etc?	|	990 Core_Pt IV-30	|	Char	|	1
ceaseoperationscd	|	Terminated?	|	990 Core_Pt IV-31	|	Char	|	1
sellorexchcd	|	Partial liquidation?	|	990 Core_Pt IV-32	|	Char	|	1
ownsepentcd	|	Disregarded entity?	|	990 Core_Pt IV-33	|	Char	|	1
reltdorgcd	|	Related entity?	|	990 Core_Pt IV-34	|	Char	|	1
intincntrlcd	|	Related organization a controlled entity?	|	990 Core_Pt IV-35	|	Char	|	1
orgtrnsfrcd	|	Any transfers to exempt non-charitable org?	|	990 Core_Pt IV-36	|	Char	|	1
conduct5percentcd	|	Activities conducted thru partnership?	|	990 Core_Pt IV-37	|	Char	|	1
compltschocd	|	Schedule O completed?	|	990 Core_Pt IV-38	|	Char	|	1
f1096cnt	|	Number forms transmitted with 1096	|	990 Core_Pt V-1a	|	Num	|	6
fw2gcnt	|	Number W-2Gs included in 1a	|	990 Core_Pt V-1b	|	Num	|	6
wthldngrulescd	|	Compliance with backup witholding?	|	990 Core_Pt V-1c	|	Char	|	1
noemplyeesw3cnt	|	Number of employees	|	990 Core_Pt V-2a	|	Num	|	6
filerqrdrtnscd	|	Employment tax returns filed?	|	990 Core_Pt V-2b	|	Char	|	1
unrelbusinccd	|	Unrelated business income?	|	990 Core_Pt V-3a	|	Char	|	1
filedf990tcd	|	Form 990-T filed?	|	990 Core_Pt V-3b	|	Char	|	1
frgnacctcd	|	Foreign financial account?	|	990 Core_Pt V-4a	|	Char	|	1
prohibtdtxshltrcd	|	Prohibited tax shelter transaction?	|	990 Core_Pt V-5a	|	Char	|	1
prtynotifyorgcd	|	Taxable party notification?	|	990 Core_Pt V-5b	|	Char	|	1
filedf8886tcd	|	Form 8886-T filed?	|	990 Core_Pt V-5c	|	Char	|	1
solicitcntrbcd	|	Non-deductible contributions?	|	990 Core_Pt V-6a	|	Char	|	1
exprstmntcd	|	Non-deduct. disclosure?	|	990 Core_Pt V-6b	|	Char	|	1
providegoodscd	|	Quid pro quo contributions?	|	990 Core_Pt V-7a	|	Char	|	1
notfydnrvalcd	|	Quid pro quo disclosure?	|	990 Core_Pt V-7b	|	Char	|	1
filedf8282cd	|	Form 8282 property disposed of?	|	990 Core_Pt V-7c	|	Char	|	1
f8282cnt	|	Number of 8282s filed	|	990 Core_Pt V-7d	|	Num	|	6
fndsrcvdcd	|	Funds to pay premiums?	|	990 Core_Pt V-7e	|	Char	|	1
premiumspaidcd	|	Premiums paid?	|	990 Core_Pt V-7f	|	Char	|	1
filedf8899cd	|	Form 8899 filed?	|	990 Core_Pt V-7g	|	Char	|	1
filedf1098ccd	|	Form 1098-C filed?	|	990 Core_Pt V-7h	|	Char	|	1
excbushldngscd	|	Excess business holdings?	|	990 Core_Pt V-8	|	Char	|	1
s4966distribcd	|	Taxable distributions?	|	990 Core_Pt V-9a	|	Char	|	1
distribtodonorcd	|	Distribution to donor?	|	990 Core_Pt V-9b	|	Char	|	1
initiationfees	|	Initiation fees amount	|	990 Core_Pt V-10a	|	Num	|	17
grsrcptspublicuse	|	Gross receipts amount	|	990 Core_Pt V-10b	|	Num	|	17
grsincmembers	|	Gross income from members	|	990 Core_Pt V-11a	|	Num	|	17
grsincother	|	Gross income from other sources	|	990 Core_Pt V-11b	|	Num	|	17
filedlieuf1041cd	|	Form 990 in lieu of 1041?	|	990 Core_Pt V-12a	|	Char	|	1
txexmptint	|	Tax exempt interest in lieu of 1041	|	990 Core_Pt V-12b	|	Num	|	17
qualhlthplncd	|	Qualified health plan in multiple states	|	990 Core_Pt V - 13a	|	Char	|	1
qualhlthreqmntn	|	Qualified health plan reserves required	|	990 Core_Pt V - 13b	|	Num	|	17
qualhlthonhnd	|	Qualified health plan reserves on hand	|	990 Core_Pt V - 13c	|	Num	|	17
rcvdpdtngcd	|	Payments for indoor tanning	|	990 Core_Pt V - 14a	|	Char	|	1
filedf720cd	|	Filed Form 720 for tanning	|	990 Core_Pt V - 14b	|	Char	|	1
totreprtabled	|	Reportable compensation from organization	|	990 Core_Pt VII-A-1d(D)	|	Num	|	17
totcomprelatede	|	Reportable compensation from related orgs	|	990 Core_Pt VII-A-1d(E)	|	Num	|	17
totestcompf	|	Other compensation	|	990 Core_Pt VII-A-1d(F)	|	Num	|	17
noindiv100kcnt	|	Number individuals greater than $100K	|	990 Core_Pt VII-A-2	|	Num	|	6
nocontractor100kcnt	|	Number of contractors greater than $100K	|	990 Core_Pt VII-B-2	|	Num	|	6
totcntrbgfts	|	Total contributions	|	990 Core_Pt VIII-1h(A)	|	Num	|	17
prgmservcode2acd	|	Program service revenue code 2a	|	990 Core_Pt VIII-2a	|	Num	|	6
totrev2acola	|	Program service revenue amount 2a	|	990 Core_Pt VIII-2a(A)	|	Num	|	17
prgmservcode2bcd	|	Program service revenue code 2b	|	990 Core_Pt VIII-2b	|	Num	|	6
totrev2bcola	|	Program service revenue amount 2b	|	990 Core_Pt VIII-2b(A)	|	Num	|	17
prgmservcode2ccd	|	Program service revenue code 2c	|	990 Core_Pt VIII-2c	|	Num	|	6
totrev2ccola	|	Program service revenue amount 2c	|	990 Core_Pt VIII-2c(A)	|	Num	|	17
prgmservcode2dcd	|	Program service revenue code 2d	|	990 Core_Pt VIII-2d	|	Num	|	6
totrev2dcola	|	Program service revenue amount 2d	|	990 Core_Pt VIII-2d(A)	|	Num	|	17
prgmservcode2ecd	|	Program service revenue code 2e	|	990 Core_Pt VIII-2e	|	Num	|	6
totrev2ecola	|	Program service revenue amount 2e	|	990 Core_Pt VIII-2e(A)	|	Num	|	17
totrev2fcola	|	Program service revenue amount 2f	|	990 Core_Pt VIII-2f(A)	|	Num	|	17
totprgmrevnue	|	Program service revenue	|	990 Core_Pt VIII-2g(A)	|	Num	|	17
invstmntinc	|	Investment income	|	990 Core_Pt VIII-3(A)	|	Num	|	17
txexmptbndsproceeds	|	Tax-exempt bond proceeds	|	990 Core_Pt VIII-4(A)	|	Num	|	17
royaltsinc	|	Royalties	|	990 Core_Pt VIII-5(A)	|	Num	|	17
grsrntsreal	|	Gross rents -- Real estate	|	990 Core_Pt VIII-6a(i)	|	Num	|	17
grsrntsprsnl	|	Gross rents -- Personal property	|	990 Core_Pt VIII-6a(ii)	|	Num	|	17
rntlexpnsreal	|	Rental expense -- Real estate	|	990 Core_Pt VIII-6b(i)	|	Num	|	17
rntlexpnsprsnl	|	Rental expense -- Personal property	|	990 Core_Pt VIII-6b(ii)	|	Num	|	17
rntlincreal	|	Net rent -- Real estate	|	990 Core_Pt VIII-6c(i)	|	Num	|	17
rntlincprsnl	|	Net rent -- Personal property	|	990 Core_Pt VIII-6c(ii)	|	Num	|	17
netrntlinc	|	Net rental income	|	990 Core_Pt VIII-6d(A)	|	Num	|	17
grsalesecur	|	Gross sales -- Securities	|	990 Core_Pt VIII-7a(i)	|	Num	|	17
grsalesothr	|	Gross sales -- Other assets	|	990 Core_Pt VIII-7a(ii)	|	Num	|	17
cstbasisecur	|	Sales expense -- Securities	|	990 Core_Pt VIII-7b(i)	|	Num	|	17
cstbasisothr	|	Sales expense -- Other assets	|	990 Core_Pt VIII-7b(ii)	|	Num	|	17
gnlsecur	|	Net gain from sales -- Securities	|	990 Core_Pt VIII-7c(i)	|	Num	|	17
gnlsothr	|	Net gain from sales -- Other assets	|	990 Core_Pt VIII-7c(ii)	|	Num	|	17
netgnls	|	Sales of assets	|	990 Core_Pt VIII-7d(A)	|	Num	|	17
grsincfndrsng	|	Gross fundraising	|	990 Core_Pt VIII-8a	|	Num	|	17
lessdirfndrsng	|	Fundraising expenses	|	990 Core_Pt VIII-8b	|	Num	|	17
netincfndrsng	|	Fundraising income	|	990 Core_Pt VIII-8c(A)	|	Num	|	17
grsincgaming	|	Gross income from gaming	|	990 Core_Pt VIII-9a	|	Num	|	17
lessdirgaming	|	Gaming expenses	|	990 Core_Pt VIII-9b	|	Num	|	17
netincgaming	|	Gaming income	|	990 Core_Pt VIII-9c(A)	|	Num	|	17
grsalesinvent	|	Gross sales of inventory	|	990 Core_Pt VIII-10a	|	Num	|	17
lesscstofgoods	|	Cost of goods sold (inventory)	|	990 Core_Pt VIII-10b	|	Num	|	17
netincsales	|	Income from sales of inventory	|	990 Core_Pt VIII-10c(A)	|	Num	|	17
miscrev11acd	|	Other revenue code 11a	|	990 Core_Pt VIII-11a	|	Num	|	6
miscrevtota	|	Other revenue amount 11a	|	990 Core_Pt VIII-11a(A)	|	Num	|	17
miscrev11bcd	|	Other revenue code 11b	|	990 Core_Pt VIII-11b	|	Num	|	6
miscrevtot11b	|	Other revenue amount 11b	|	990 Core_Pt VIII-11b(A)	|	Num	|	17
miscrev11ccd	|	Other revenue code 11c	|	990 Core_Pt VIII-11c	|	Num	|	6
miscrevtot11c	|	Other revenue amount 11c	|	990 Core_Pt VIII-11c(A)	|	Num	|	17
miscrevtot11d	|	Other revenue amount 11d	|	990 Core_Pt VIII-11d(A)	|	Num	|	17
miscrevtot11e	|	Other revenue	|	990 Core_Pt VIII-11e(A)	|	Num	|	17
totrevenue	|	Total revenue	|	990 Core_Pt VIII-12(A)	|	Num	|	17
grntstogovt	|	Grants to governments/orgs in the US	|	990 Core_Pt IX-1(A)	|	Num	|	17
grnsttoindiv	|	Grants to individuals in the US	|	990 Core_Pt IX-2(A)	|	Num	|	17
grntstofrgngovt	|	Grants to orgs and individuals outside the US	|	990 Core_Pt IX-3(A)	|	Num	|	17
benifitsmembrs	|	Benefits paid to or for members	|	990 Core_Pt IX-4(A)	|	Num	|	17
compnsatncurrofcr	|	Compensation of current officers, directors, etc 	|	990 Core_Pt IX-5(A)	|	Num	|	17
compnsatnandothr	|	Compensation of disqualified persons	|	990 Core_Pt IX-6(A)	|	Num	|	17
othrsalwages	|	Other salaries and wages	|	990 Core_Pt IX-7(A)	|	Num	|	17
pensionplancontrb	|	Pension plan contributions	|	990 Core_Pt IX-8(A)	|	Num	|	17
othremplyeebenef	|	Other employee benefits	|	990 Core_Pt IX-9(A)	|	Num	|	17
payrolltx	|	Payroll taxes	|	990 Core_Pt IX-10(A)	|	Num	|	17
feesforsrvcmgmt	|	Management fees	|	990 Core_Pt IX-11a(A)	|	Num	|	17
legalfees	|	Legal fees	|	990 Core_Pt IX-11b(A)	|	Num	|	17
accntingfees	|	Accounting fees	|	990 Core_Pt IX-11c(A)	|	Num	|	17
feesforsrvclobby	|	Lobbying fees	|	990 Core_Pt IX-11d(A)	|	Num	|	17
profndraising	|	Professional fundraising fees	|	990 Core_Pt IX-11e(A)	|	Num	|	17
feesforsrvcinvstmgmt	|	Investment management feed	|	990 Core_Pt IX-11f(A)	|	Num	|	17
feesforsrvcothr	|	Other fees	|	990 Core_Pt IX-11g(A)	|	Num	|	17
advrtpromo	|	Advertising and promotion	|	990 Core_Pt IX-12(A)	|	Num	|	17
officexpns	|	Office expenses	|	990 Core_Pt IX-13(A)	|	Num	|	17
infotech	|	Information technology	|	990 Core_Pt IX-14(A)	|	Num	|	17
royaltsexpns	|	Royalties	|	990 Core_Pt IX-15(A)	|	Num	|	17
occupancy	|	Occupancy	|	990 Core_Pt IX-16(A)	|	Num	|	17
travel	|	Travel	|	990 Core_Pt IX-17(A)	|	Num	|	17
travelofpublicoffcl	|	Travel/entertainment expenses to public officials	|	990 Core_Pt IX-18(A)	|	Num	|	17
converconventmtng	|	Conferences, conventions, meetings	|	990 Core_Pt IX-19(A)	|	Num	|	17
interestamt	|	Interest expense	|	990 Core_Pt IX20(A)	|	Num	|	17
pymtoaffiliates	|	Payments to affiliates	|	990 Core_Pt IX-21(A)	|	Num	|	17
deprcatndepletn	|	Depreciation, depletion, amortization	|	990 Core_Pt IX-22(A)	|	Num	|	17
insurance	|	Insurance	|	990 Core_Pt IX-23(A)	|	Num	|	17
othrexpnsa	|	Other expenses 24a	|	990 Core_Pt IX-24a(A)	|	Num	|	17
othrexpnsb	|	Other expenses 24b	|	990 Core_Pt IX-24b(A)	|	Num	|	17
othrexpnsc	|	Other expenses 24c	|	990 Core_Pt IX-24c(A)	|	Num	|	17
othrexpnsd	|	Other expenses 24d	|	990 Core_Pt IX-24d(A)	|	Num	|	17
othrexpnse	|	Other expenses 24e	|	990 Core_Pt IX-24e(A)	|	Num	|	17
othrexpnsf	|	Other expenses 24f	|	990 Core_Pt IX-24f(A)	|	Num	|	17
totfuncexpns	|	Total functional expenses	|	990 Core_Pt IX-25(A)	|	Num	|	17
nonintcashend	|	Cash -- non-interest bearing -- eoy	|	990 Core_Pt X-1(B)	|	Num	|	17
svngstempinvend	|	Savings and temporary cash investments -- eoy	|	990 Core_Pt X-2(B)	|	Num	|	17
pldgegrntrcvblend	|	Pledges and grants receivable -- eoy	|	990 Core_Pt X-3(B)	|	Num	|	17
accntsrcvblend	|	Accounts receivable -- eoy	|	990 Core_Pt X-4(B)	|	Num	|	17
currfrmrcvblend	|	Receivables from officers, directors, etc. -- eoy	|	990 Core_Pt X-5(B)	|	Num	|	17
rcvbldisqualend	|	Receivables from disqualified persons -- eoy	|	990 Core_Pt X-6(B)	|	Num	|	17
notesloansrcvblend	|	Notes and loans receivables -- eoy	|	990 Core_Pt X-7(B)	|	Num	|	17
invntriesalesend	|	Inventories for sale or use -- eoy	|	990 Core_Pt X-8(B)	|	Num	|	17
prepaidexpnsend	|	Prepaid expenses or deferred charges -- eoy	|	990 Core_Pt X-9(B)	|	Num	|	17
lndbldgsequipend	|	Land, buildings, & equipment (net) -- eoy	|	990 Core_Pt X-10(B)	|	Num	|	17
invstmntsend	|	Investments in publicly traded securities -- eoy	|	990 Core_Pt X-11(B)	|	Num	|	17
invstmntsothrend	|	Investments in other securities -- eoy	|	990 Core_Pt X-12(B)	|	Num	|	17
invstmntsprgmend	|	Program-related investments -- eoy	|	990 Core_Pt X-13(B)	|	Num	|	17
intangibleassetsend	|	Intangible assets -- eoy	|	990 Core_Pt X-14(B)	|	Num	|	17
othrassetsend	|	Other assets -- eoy	|	990 Core_Pt X-15(B)	|	Num	|	17
totassetsend	|	Total assets -- eoy	|	990 Core_Pt X-16(B)	|	Num	|	17
accntspayableend	|	Accounts payable and accrued expenses -- eoy	|	990 Core_Pt X-17(B)	|	Num	|	17
grntspayableend	|	Grants payable -- eoy	|	990 Core_Pt X-18(B)	|	Num	|	17
deferedrevnuend	|	Deferred revenue -- eoy	|	990 Core_Pt X-19(B)	|	Num	|	17
txexmptbndsend	|	Tax-exempt bond liabilities -- eoy	|	990 Core_Pt X-20(B)	|	Num	|	17
escrwaccntliabend	|	Escrow account liability -- eoy	|	990 Core_Pt X-21(B)	|	Num	|	17
paybletoffcrsend	|	Payables to officers, directors, etc. -- eoy	|	990 Core_Pt X-22(B)	|	Num	|	17
secrdmrtgsend	|	Secured mortgages and notes payable -- eoy	|	990 Core_Pt X-23(B)	|	Num	|	17
unsecurednotesend	|	Unsecured mortgages and notes payable -- eoy	|	990 Core_Pt X-24(B)	|	Num	|	17
othrliabend	|	Other liabilities -- eoy	|	990 Core_Pt X-25(B)	|	Num	|	17
totliabend	|	Total liabilities -- eoy	|	990 Core_Pt X-26(B)	|	Num	|	17
unrstrctnetasstsend	|	Unrestricted net assets -- eoy	|	990 Core_Pt X-27(B)	|	Num	|	17
temprstrctnetasstsend	|	Temporarily restricted net assets -- eoy	|	990 Core_Pt X-28(B)	|	Num	|	17
permrstrctnetasstsend	|	Permanently restricted net assets -- eoy	|	990 Core_Pt X-29(B)	|	Num	|	17
capitalstktrstend	|	Capital stock or trust principal -- eoy	|	990 Core_Pt X-30(B)	|	Num	|	17
paidinsurplusend	|	Paid-in or capital surplus -- eoy	|	990 Core_Pt X-31(B)	|	Num	|	17
retainedearnend	|	Retained earnings -- eoy	|	990 Core_Pt X-32(B)	|	Num	|	17
totnetassetend	|	Total Net Assets -- eoy	|	990 Core_Pt X-33(B)	|	Num	|	17
totnetliabastend	|	Total Liabilities + Net Assets -- eoy	|	990 Core_Pt X-34(B)	|	Num	|	17
nonpfrea	|	Reason for non-PF status	|	990 Sch A_Pt I-1-11	|	Num	|	2
totnooforgscnt	|	Number of organizations supported	|	990 Sch A_Pt I-11h	|	Num	|	6
totsupport	|	Sum of amounts of support	|	990 Sch A_Pt I-11h(vii)	|	Num	|	17
gftgrntsrcvd170	|	Gifts grants membership fees received (170)	|	990 Sch A_Pt II-1(f)	|	Num	|	17
txrevnuelevied170	|	Tax revenues levied (170)	|	990 Sch A_Pt II-2(f)	|	Num	|	17
srvcsval170	|	Services or facilities furnished by gov (170)	|	990 Sch A_Pt II-3(f)	|	Num	|	17
pubsuppsubtot170	|	Public support subtotal (170)	|	990 Sch A_Pt II-4(f)	|	Num	|	17
exceeds2pct170	|	Amount support exceeds total (170)	|	990 Sch A_Pt II-5(f)	|	Num	|	17
pubsupplesspct170	|	Public support (170)	|	990 Sch A_Pt II-6(f)	|	Num	|	17
samepubsuppsubtot170	|	Public support from line 4 (170)	|	990 Sch A_Pt II-7(f)	|	Num	|	17
grsinc170	|	Gross income from interest etc (170)	|	990 Sch A_Pt II-8(f)	|	Num	|	17
netincunreltd170	|	Net UBI (170)	|	990 Sch A_Pt II-9(f)	|	Num	|	17
othrinc170	|	Other income (170)	|	990 Sch A_Pt II-10(f)	|	Num	|	17
totsupp170	|	Total support (170)	|	990 Sch A_Pt II-11(f)	|	Num	|	17
grsrcptsrelated170	|	Gross receipts from related activities (170)	|	990 Sch A_Pt II-12	|	Num	|	17
totgftgrntrcvd509	|	Gifts grants membership fees received (509)	|	990 Sch A_Pt III-1(f)	|	Num	|	17
grsrcptsadmissn509	|	Receipts from admissions merchandise etc (509)	|	990 Sch A_Pt III-2(f)	|	Num	|	17
grsrcptsactivities509	|	Gross receipts from related activities (509)	|	990 Sch A_Pt III-3(f)	|	Num	|	17
txrevnuelevied509	|	Tax revenues levied (509)	|	990 Sch A_Pt III-4(f)	|	Num	|	17
srvcsval509	|	Services or facilities furnished by gov (509)	|	990 Sch A_Pt III-5(f)	|	Num	|	17
pubsuppsubtot509	|	Public support subtotal (509)	|	990 Sch A_Pt III-6(f)	|	Num	|	17
rcvdfrmdisqualsub509	|	Amounts from disqualified persons (509)	|	990 Sch A_Pt III-7a(f)	|	Num	|	17
exceeds1pct509	|	Amount support exceeds total (509)	|	990 Sch A_Pt III-7b(f)	|	Num	|	17
subtotpub509	|	Public support subtotal (509)	|	990 Sch A_Pt III-7c(f)	|	Num	|	17
pubsupplesub509	|	Public support (509)	|	990 Sch A_Pt III-8(f)	|	Num	|	17
samepubsuppsubtot509	|	Public support from line 6 (509)	|	990 Sch A_Pt III-9(f)	|	Num	|	17
grsinc509	|	Gross income from interest etc (509)	|	990 Sch A_Pt III-10a(f)	|	Num	|	17
unreltxincls511tx509	|	Net UBI (509)	|	990 Sch A_Pt III-10b(f)	|	Num	|	17
subtotsuppinc509	|	Subtotal total support (509)	|	990 Sch A_Pt III-10c(f)	|	Num	|	17
netincunrelatd509	|	Net income from UBI not in 10b (509)	|	990 Sch A_Pt III-11(f)	|	Num	|	17
othrinc509	|	Other income (509)	|	990 Sch A_Pt III-12(f)	|	Num	|	17
totsupp509	|	Total support (509)	|	990 Sch A_Pt III-13(f)	|	Num	|	17





## 2015 990EZ DATA DICTIONARY


ELEMENT NAME	|	DESCRIPTION	|	LOCATION	|	TYPE	|	LENGTH
----------------|-----------------------|-----------------------|---------------|--------------------------------
elf	|	E-file indicator	|	n/a	|	Char	|	1
EIN	|	Employer Identification Number	|	Form 990-EZ Header	|	Num	|	9
tax_pd	|	Tax period	|	Form 990-EZ Header	|	Num	|	6
subseccd	|	Subsection code	|	Form 990-EZ Header	|	Num	|	2
totcntrbs	|	Contributions, gifts, grants, etc received	|	990-EZ_Pt I-1	|	Num	|	17
prgmservrev	|	Program service revenue	|	990-EZ_Pt I-2	|	Num	|	17
duesassesmnts	|	Membership dues and assessments	|	990-EZ_Pt I-3	|	Num	|	17
othrinvstinc	|	Investment income	|	990-EZ_Pt I-4	|	Num	|	17
grsamtsalesastothr	|	Gross amount from sale of assets 	|	990-EZ_Pt I-5a	|	Num	|	17
basisalesexpnsothr	|	Cost or other basis and sales expenses	|	990-EZ_Pt I-5b	|	Num	|	17
gnsaleofastothr	|	Gain or (loss) from sale of assets	|	990-EZ_Pt I-5c	|	Num	|	17
grsincgaming	|	Gross income from gaming	|	990-EZ_Pt I-6a	|	Num	|	17
grsrevnuefndrsng	|	Special events gross revenue	|	990-EZ_Pt I-6b	|	Num	|	17
direxpns	|	Special events direct expenses	|	990-EZ_Pt I-6c	|	Num	|	17
netincfndrsng	|	Special events net income (or loss)	|	990-EZ_Pt I-6d	|	Num	|	17
grsalesminusret	|	Gross sales of inventory	|	990-EZ_Pt I-7a	|	Num	|	17
costgoodsold	|	Less: cost of goods sold	|	990-EZ_Pt I-7b	|	Num	|	17
grsprft	|	Gross profit (or loss) from sales of inventory	|	990-EZ_Pt I-7c	|	Num	|	17
othrevnue	|	Other revenue - total	|	990-EZ_Pt I-8	|	Num	|	17
totrevnue	|	Total revenue	|	990-EZ_Pt I-9	|	Num	|	17
totexpns	|	Total expenses	|	990-EZ_Pt I-17	|	Num	|	17
totexcessyr	|	Excess or deficit	|	990-EZ_Pt I-18	|	Num	|	17
othrchgsnetassetfnd	|	Other changes in net assets	|	990-EZ_Pt I-20	|	Num	|	17
networthend	|	Net assets EOY	|	990-EZ_Pt I-21	|	Num	|	17
totassetsend	|	Total assets e-o-y	|	990-EZ_Pt II-25B	|	Num	|	17
totliabend	|	Total liabilities e-o-y	|	990-EZ_Pt II-26B	|	Num	|	17
totnetassetsend	|	Total net worth e-o-y	|	990-EZ_Pt II-27B	|	Num	|	17
actvtynotprevrptcd	|	Activity not previously reported?	|	990-EZ_Pt V-33	|	Char	|	1
chngsinorgcd	|	Significant changes to governing docs?	|	990-EZ_Pt V-34	|	Char	|	1
unrelbusincd	|	UBI over $1,000?	|	990-EZ_Pt V-35a	|	Char	|	1
filedf990tcd	|	Organization Filed 990T	|	990-EZ_Pt V-35b	|	Char	|	1
contractioncd	|	Liquidation, dissolution, termination, or contraction	|	990-EZ_Pt V-36	|	Char	|	1
politicalexpend	|	Direct or indirect political expenditures.	|	990-EZ_Pt V-37a	|	Num	|	17
filedf1120polcd	|	File Form 1120-POL?	|	990-EZ_Pt V-37b	|	Char	|	1
loanstoofficerscd	|	Loans to/from officers, directors or trustees?	|	990-EZ_Pt V-38a	|	Char	|	1
loanstoofficers	|	Amount of loans to/from officers	|	990-EZ_Pt V-38b	|	Num	|	17
initiationfee	|	Initiation fees and capital contributions	|	990-EZ_Pt V-39a	|	Num	|	17
grspublicrcpts	|	Gross receipts for public use of club facilities	|	990-EZ_Pt V-39b	|	Num	|	17
s4958excessbenefcd	|	Section 4958 excess benefit transactions?	|	990-EZ_Pt V-40b	|	Char	|	1
prohibtdtxshltrcd	|	Party to a prohibited tax shelter transaction?	|	990-EZ_Pt V-40e	|	Char	|	1
nonpfrea	|	Reason for non-PF status	|	990-EZ Sch A_Pt I-1-11	|	Num	|	2
totnooforgscnt	|	Number of organizations supported	|	990-EZ Sch A_Pt I-11h	|	Num	|	6
totsupport	|	Sum of amounts of support	|	990-EZ Sch A_Pt I-11h(vii)	|	Num	|	17
gftgrntsrcvd170	|	Gifts grants membership fees received (170)	|	990-EZ Sch A_Pt II-1(f)	|	Num	|	17
txrevnuelevied170	|	Tax revenues levied (170)	|	990-EZ Sch A_Pt II-2(f)	|	Num	|	17
srvcsval170	|	Services or facilities furnished by gov (170)	|	990-EZ Sch A_Pt II-3(f)	|	Num	|	17
pubsuppsubtot170	|	Public support subtotal (170)	|	990-EZ Sch A_Pt II-4(f)	|	Num	|	17
exceeds2pct170	|	Amount support exceeds total (170)	|	990-EZ Sch A_Pt II-5(f)	|	Num	|	17
pubsupplesspct170	|	Public support (170)	|	990-EZ Sch A_Pt II-6(f)	|	Num	|	17
samepubsuppsubtot170	|	Public support from line 4 (170)	|	990-EZ Sch A_Pt II-7(f)	|	Num	|	17
grsinc170	|	Gross income from interest etc (170)	|	990-EZ Sch A_Pt II-8(f)	|	Num	|	17
netincunreltd170	|	Net UBI (170)	|	990-EZ Sch A_Pt II-9(f)	|	Num	|	17
othrinc170	|	Other income (170)	|	990-EZ Sch A_Pt II-10(f)	|	Num	|	17
totsupp170	|	Total support (170)	|	990-EZ Sch A_Pt II-11(f)	|	Num	|	17
grsrcptsrelated170	|	Gross receipts from related activities (170)	|	990-EZ Sch A_Pt II-12	|	Num	|	17
totgftgrntrcvd509	|	Gifts grants membership fees received (509)	|	990-EZ Sch A_Pt III-1(f)	|	Num	|	17
grsrcptsadmissn509	|	Receipts from admissions merchandise etc (509)	|	990-EZ Sch A_Pt III-2(f)	|	Num	|	17
grsrcptsactivities509	|	Gross receipts from related activities (509)	|	990-EZ Sch A_Pt III-3(f)	|	Num	|	17
txrevnuelevied509	|	Tax revenues levied (509)	|	990-EZ Sch A_Pt III-4(f)	|	Num	|	17
srvcsval509	|	Services or facilities furnished by gov (509)	|	990-EZ Sch A_Pt III-5(f)	|	Num	|	17
pubsuppsubtot509	|	Public support subtotal (509)	|	990-EZ Sch A_Pt III-6(f)	|	Num	|	17
rcvdfrmdisqualsub509	|	Amounts from disqualified persons (509)	|	990-EZ Sch A_Pt III-7a(f)	|	Num	|	17
exceeds1pct509	|	Amount support exceeds total (509)	|	990-EZ Sch A_Pt III-7b(f)	|	Num	|	17
subtotpub509	|	Public support subtotal (509)	|	990-EZ Sch A_Pt III-7c(f)	|	Num	|	17
pubsupplesub509	|	Public support (509)	|	990-EZ Sch A_Pt III-8(f)	|	Num	|	17
samepubsuppsubtot509	|	Public support from line 6 (509)	|	990-EZ Sch A_Pt III-9(f)	|	Num	|	17
grsinc509	|	Gross income from interest etc (509)	|	990-EZ Sch A_Pt III-10a(f)	|	Num	|	17
unreltxincls511tx509	|	Net UBI (509)	|	990-EZ Sch A_Pt III-10b(f)	|	Num	|	17
subtotsuppinc509	|	Subtotal total support (509)	|	990-EZ Sch A_Pt III-10c(f)	|	Num	|	17
netincunrelatd509	|	Net income from UBI not in 10b (509)	|	990-EZ Sch A_Pt III-11(f)	|	Num	|	17
othrinc509	|	Other income (509)	|	990-EZ Sch A_Pt III-12(f)	|	Num	|	17
totsupp509	|	Total support (509)	|	990-EZ Sch A_Pt III-13(f)	|	Num	|	17




## 2015 990-PF DATA DICTIONARY




ELEMENT NAME	|	DESCRIPTION	|	LOCATION	|	TYPE	|	LENGTH
----------------|-----------------------|-----------------------|---------------|--------------------------------
elf	|	E-file indicator	|	n/a	|	Char	|	1
ein	|	Employer Identification Number	|	Form 990-PF, Item A	|	Num	|	9
tax_prd	|	Tax period (YYYYMM format)	|	Top of form	|	Char	|	6
eostatus	|	EO Status Code	|	n/a (IRS-Coded)	|	Char	|	2
tax_yr	|	SOI Year	|	990-PF Header	|	Num	|	4
operatingcd	|	Operating foundation code	|	n/a (IRS-Coded)	|	Char	|	1
subcd	|	Subsection code	|	n/a (IRS-Coded)	|	Char	|	2
fairmrktvalamt	|	Total assets – e-o-y fair market value 	|	990-PF Header, Item I	|	Num	|	15
grscontrgifts	|	Contributions received	|	990-PF Pt I Line 1, col (a)	|	Num	|	15
schedbind	|	Schedule B indicator	|	n/a (IRS-Coded based on presence of Schedule B contributor information)	|	Char	|	1
intrstrvnue	|	Interest revenue	|	990-PF Pt I Line 3, col (a)	|	Num	|	15
dividndsamt	|	Dividends	|	990-PF Pt I Line 4, col (a)	|	Num	|	15
grsrents	|	Gross rents	|	990-PF Pt I-5a, col (a)	|	Num	|	15
grsslspramt	|	Gross sales price for assets 	|	990-PF Pt I-6b	|	Num	|	15
costsold	|	Cost-of-goods-sold	|	990-PF Pt I-10b	|	Num	|	15
grsprofitbus	|	Gross profit	|	990-PF Pt I-10c, col (a)	|	Num	|	15
otherincamt	|	Other income	|	990-PF Pt I-11, col (a)	|	Num	|	15
totrcptperbks	|	Total revenue	|	990-PF Pt I-12, col (a)	|	Num	|	15
compofficers	|	Compensation of officers	|	990-PF Pt I-13, col (a)	|	Num	|	15
pensplemplbenf	|	Pension plans, employee benefits 	|	990-PF Pt I-15, col (a)	|	Num	|	15
legalfeesamt	|	Legal fees	|	990-PF Pt I-16a, col (a)	|	Num	|	15
accountingfees	|	Accounting fees	|	990-PF Pt I-16b, col (a)	|	Num	|	15
interestamt	|	Interest	|	990-PF Pt I-17, col (a)	|	Num	|	15
depreciationamt	|	Depreciation and depletion	|	990-PF Pt I-19, col (a)	|	Num	|	15
occupancyamt	|	Occupancy	|	990-PF Pt I-20, col (a)	|	Num	|	15
travlconfmtngs	|	Travel, conferences, and meetings	|	990-PF Pt I-21, col (a)	|	Num	|	15
printingpubl	|	Printing and publications	|	990-PF Pt I-22, col (a)	|	Num	|	15
topradmnexpnsa	|	Total operating and administrative expenses column a 	|	990-PF Pt I-24, col (a)	|	Num	|	15
contrpdpbks	|	Contributions, gifts, grants paid	|	990-PF Pt I-25, col (a)	|	Num	|	15
totexpnspbks	|	Total expenses	|	990-PF Pt I-26, col (a)	|	Num	|	15
excessrcpts	|	Net income less deficit	|	990-PF Pt I-27a	|	Num	|	15
totrcptnetinc	|	Total receipts net investment income	|	990-PF Pt I-12, col (b)	|	Num	|	15
topradmnexpnsb	|	Total operating and administrative expenses column b 	|	990-PF Pt I-24, col (b)	|	Num	|	15
totexpnsnetinc	|	Total expenses net investment income	|	990-PF Pt I-26, col (b)	|	Num	|	15
netinvstinc	|	Net investment income	|	990-PF Pt I-27b	|	Num	|	15
trcptadjnetinc	|	Total receipts adjusted net income	|	990-PF Pt I-12, col (c)	|	Num	|	15
totexpnsadjnet	|	Total expenses adjusted net income	|	990-PF Pt I-26, col (c)	|	Num	|	15
adjnetinc	|	Adjusted net income	|	990-PF Pt I-27c	|	Num	|	15
topradmnexpnsd	|	Total operating and administrative expenses column d	|	990-PF Pt I-24, col (d)	|	Num	|	15
totexpnsexempt	|	Total expenses – exempt purpose	|	990-PF Pt I-26, col (d)	|	Num	|	15
othrcashamt	|	Cash non-interest-bearing – e-o-y book value	|	990-PF Pt II-1, col (b)	|	Num	|	15
invstgovtoblig	|	Investments in U.S. & state government obligations – e-o-y book value	|	990-PF Pt II-10a, col (b)	|	Num	|	15
invstcorpstk	|	Investments in corporate stock – e-o-y book value	|	990-PF Pt II-10b, col (b)	|	Num	|	15
invstcorpbnd	|	Investments in corporate bonds– e-o-y book value	|	990-PF Pt II-10c, col (b)	|	Num	|	15
totinvstsec	|	Total investments in securities – e-o-y book value	|	990-PF Pt II, Lines 10a+10b+10c, col (b)	|	Num	|	15
mrtgloans	|	Investments mortgage loans – e-o-y book value	|	990-PF Pt II-12, col (b)	|	Num	|	15
othrinvstend	|	Other investments – e-o-y book value	|	990-PF Pt II-13, col (b)	|	Num	|	15
othrassetseoy	|	Other assets – e-o-y book value	|	990-PF Pt II-15, col (b)	|	Num	|	15
totassetsend	|	Total assets – e-o-y book value	|	990-PF Pt II-16, col (b)	|	Num	|	15
mrtgnotespay	|	Mortgage loans payable – e-o-y book value	|	990-PF Pt II-21, col (b)	|	Num	|	15
othrliabltseoy	|	Other liabilities – e-o-y book value	|	990-PF Pt II-22, col (b)	|	Num	|	15
totliabend	|	Total liabilities – e-o-y book value	|	990-PF Pt II-23, col (b)	|	Num	|	15
tfundnworth	|	Total fund net worth – e-o-y book value	|	990-PF Pt II-31, col (b)	|	Num	|	15
fairmrktvaleoy	|	Total assets – e-o-y fair market value 	|	990-PF Pt II-16, col (c)	|	Num	|	15
totexcapgnls	|	Capital gain net income	|	990-PF Pt IV-2	|	Num	|	15
totexcapgn	|	Net gain – sales of assets	|	990-PF Part IV-2 > 0	|	Num	|	15
totexcapls	|	Net loss – sales of assets	|	990-PF Part IV-2 < 0	|	Num	|	15
invstexcisetx	|	Excise tax on net investment income	|	990-PF Pt VI-1	|	Num	|	15
sec4940notxcd	|	Section 4940 – no tax	|	990-PF Pt VI-1b not checked	|	Num	|	1
sec4940redtxcd	|	Section 4940 – 1 % tax	|	990-PF Pt VI-1b checked	|	Num	|	1
sect511tx	|	Section 511 tax	|	990-PF Pt VI-2	|	Num	|	15
subtitleatx	|	Subtitle A tax	|	990-PF Pt VI-4	|	Num	|	15
totaxpyr	|	Total excise tax	|	990-PF Pt VI-5	|	Num	|	15
esttaxcr	|	Estimated tax credit	|	990-PF Pt VI-6a	|	Num	|	15
txwithldsrc	|	Tax withheld at source	|	990-PF Pt VI-6b	|	Num	|	15
txpaidf2758	|	Tax paid with Form 2758 (filing extension)	|	990-PF Pt VI-6c	|	Num	|	15
erronbkupwthld	|	Erroneous backup withholding credit amount	|	990-PF Pt VI-6d	|	Num	|	15
estpnlty	|	Estimated tax penalty	|	990-PF Pt VI-8	|	Num	|	15
taxdue	|	Tax due 	|	990-PF Pt VI-9 	|	Num	|	15
overpay	|	Overpayment	|	990-PF Pt VI-10 	|	Num	|	15
crelamt	|	Credit elect amount	|	990-PF Pt VI-11	|	Num	|	15
infleg	|	Influence legislation?	|	990-PF Pt VII-A-1a	|	Char	|	1
actnotpr	|	Activities not previously reported?	|	990-PF Pt VII-A-2	|	Char	|	1
chgnprvrptcd	|	Changes not previously reported?	|	990-PF Pt VII-A-3	|	Char	|	1
filedf990tcd	|	Filed 990-T?	|	990-PF Pt VII-A-4b	|	Char	|	1
contractncd	|	Contraction?	|	990-PF Pt VII-A-5	|	Char	|	1
furnishcpycd	|	Furnished copy to Attorney General?	|	990-PF Pt VII-A-8b	|	Char	|	1
claimstatcd	|	Claiming status?	|	990-PF Pt VII-A-9	|	Char	|	1
cntrbtrstxyrcd	|	Substantial contributors?	|	990-PF Pt VII-A-10	|	Char	|	1
distribdafcd	|	Distribution to donor advised fund with advisory privileges?	|	990-PF Pt VII-A-12	|	Char	|	1
orgcmplypubcd	|	Comply with public inspection?	|	990-PF Pt VII-A-13	|	Char	|	1
filedlf1041ind	|	Section 4947(a)(1) filing in lieu of Form 1041?	|	990-PF Pt VII-A-15	|	Char	|	1
propexchcd	|	Property exchange?	|	990-PF Pt VII-B-1a(1)	|	Char	|	1
brwlndmnycd	|	Borrow lend money?	|	990-PF Pt VII-B-1a(2)	|	Char	|	1
furngoodscd	|	Furnished goods?	|	990-PF Pt VII-B-1a(3)	|	Char	|	1
paidcmpncd	|	Paid compensation?	|	990-PF Pt VII-B-1a(4)	|	Char	|	1
transfercd	|	Transfer?	|	990-PF Pt VII-B-1a(5)	|	Char	|	1
agremkpaycd	|	Agree to make pay?	|	990-PF Pt VII-B-1a(6)	|	Char	|	1
exceptactsind	|	Acts fail to qualify under section 53.4941(d)-3?	|	990-PF Pt VII-B-1b	|	Char	|	1
prioractvcd	|	Engage in acts in prior year?	|	990-PF Pt VII-B-1c	|	Char	|	1
undistrinccd	|	Undistributed income?	|	990-PF Pt VII-B-2a	|	Char	|	1
applyprovind	|	Not applying section 4942(a)(2) provisions?	|	990-PF Pt VII-B-2b	|	Char	|	1
dirindirintcd	|	Direct indirect interest?	|	990-PF Pt VII-B-3a	|	Char	|	1
excesshldcd	|	Excess business holdings?	|	990-PF Pt VII-B-3b	|	Char	|	1
invstjexmptcd	|	Jeopardizing investments?	|	990-PF Pt VII-B-4a	|	Char	|	1
prevjexmptcd	|	Prior year jeopardizing investments?	|	990-PF Pt VII-B-4b	|	Char	|	1
propgndacd	|	Propaganda?	|	990-PF Pt VII-B-5a(1)	|	Char	|	1
ipubelectcd	|	Influence public election?	|	990-PF Pt VII-B-5a(2)	|	Char	|	1
grntindivcd	|	Grant individual?	|	990-PF Pt VII-B-5a(3)	|	Char	|	1
nchrtygrntcd	|	Non-charity grant?	|	990-PF Pt VII-B-5a(4)	|	Char	|	1
nreligiouscd	|	Non-religious?	|	990-PF Pt VII-B-5a(5)	|	Char	|	1
excptransind	|	Transactions fail to qualify under section 53.4945?	|	990-PF Pt VII-B-5b	|	Char	|	1
rfprsnlbnftind	|	Receive funds to pay premiums on personal benefit contract?	|	990-PF Pt VII-B-6a	|	Char	|	1
pyprsnlbnftind	|	Pay premiums on personal benefit contract?	|	990-PF Pt VII-B-6b	|	Char	|	1
tfairmrktunuse	|	Fair market value of assets not used for charitable purposes 	|	990-PF Pt X-1d	|	Num	|	15
valncharitassets	|	Net value of noncharitable-use assets	|	990-PF Pt X-5	|	Num	|	15
cmpmininvstret	|	Minimum investment return	|	990-PF Pt X-6	|	Num	|	15
distribamt	|	Distributable amount	|	990-PF Pt XI-7	|	Num	|	15
undistribincyr	|	Undistributed income	|	990-PF Pt XIII-6f, col (d)	|	Num	|	15
adjnetinccola	|	Adjusted net income column a	|	990-PF Pt XIV-2a, col (a)	|	Num	|	15
adjnetinccolb	|	Adjusted net income column b	|	990-PF Pt XIV-2a, col (b)	|	Num	|	15
adjnetinccolc	|	Adjusted net income column c	|	990-PF Pt XIV-2a, col (c)	|	Num	|	15
adjnetinccold	|	Adjusted net income column d	|	990-PF Pt XIV-2a, col (d)	|	Num	|	15
adjnetinctot	|	Adjusted net income total	|	990-PF Pt XIV-2a, col (e)	|	Num	|	15
qlfydistriba	|	Qualifying distributions column a	|	990-PF Pt XIV-2e, col (a)	|	Num	|	15
qlfydistribb	|	Qualifying distributions column b	|	990-PF Pt XIV-2e, col (b)	|	Num	|	15
qlfydistribc	|	Qualifying distributions column c	|	990-PF Pt XIV-2e, col (c)	|	Num	|	15
qlfydistribd	|	Qualifying distributions column d	|	990-PF Pt XIV-2e, col (d)	|	Num	|	15
qlfydistribtot	|	Qualifying distributions total	|	990-PF Pt XIV-2e, col (e)	|	Num	|	15
valassetscola	|	Value assets column a	|	990-PF Pt XIV-3a(1), col (a)	|	Num	|	15
valassetscolb	|	Value assets column b	|	990-PF Pt XIV-3a(1), col (b)	|	Num	|	15
valassetscolc	|	Value assets column c	|	990-PF Pt XIV-3a(1), col (c)	|	Num	|	15
valassetscold	|	Value assets column d	|	990-PF Pt XIV-3a(1), col (d)	|	Num	|	15
valassetstot	|	Value assets total	|	990-PF Pt XIV-3a(1), col (e)	|	Num	|	15
qlfyasseta	|	Qualifying assets column a	|	990-PF Pt XIV-3a(2), col (a)	|	Num	|	15
qlfyassetb	|	Qualifying assets column b	|	990-PF Pt XIV-3a(2), col (b)	|	Num	|	15
qlfyassetc	|	Qualifying assets column c	|	990-PF Pt XIV-3a(2), col (c)	|	Num	|	15
qlfyassetd	|	Qualifying assets column d	|	990-PF Pt XIV-3a(2), col (d)	|	Num	|	15
qlfyassettot	|	Qualifying assets total	|	990-PF Pt XIV-3a(2), col (e)	|	Num	|	15
endwmntscola	|	Endowments column a	|	990-PF Pt XIV-3b, col (a)	|	Num	|	15
endwmntscolb	|	Endowments column b	|	990-PF Pt XIV-3b, col (b)	|	Num	|	15
endwmntscolc	|	Endowments column c	|	990-PF Pt XIV-3b, col (c)	|	Num	|	15
endwmntscold	|	Endowments column d	|	990-PF Pt XIV-3b, col (d)	|	Num	|	15
endwmntstot	|	Endowments total	|	990-PF Pt XIV-3b, col (e)	|	Num	|	15
totsuprtcola	|	Total support column a	|	990-PF Pt XIV-3c(1), col (a)	|	Num	|	15
totsuprtcolb	|	Total support column b	|	990-PF Pt XIV-3c(1), col (b)	|	Num	|	15
totsuprtcolc	|	Total support column c	|	990-PF Pt XIV-3c(1), col (c)	|	Num	|	15
totsuprtcold	|	Total support column d	|	990-PF Pt XIV-3c(1), col (d)	|	Num	|	15
totsuprttot	|	Total support total	|	990-PF Pt XIV-3c(1), col (e)	|	Num	|	15
pubsuprtcola	|	Public support column a	|	990-PF Pt XIV-3c(2), col (a)	|	Num	|	15
pubsuprtcolb	|	Public support column b	|	990-PF Pt XIV-3c(2), col (b)	|	Num	|	15
pubsuprtcolc	|	Public support column c	|	990-PF Pt XIV-3c(2), col (c)	|	Num	|	15
pubsuprtcold	|	Public support column d	|	990-PF Pt XIV-3c(2), col (d)	|	Num	|	15
pubsuprttot	|	Public support total	|	990-PF Pt XIV-3c(2), col (e)	|	Num	|	15
grsinvstinca	|	Gross investment income column a	|	990-PF Pt XIV-3c(4), col (a)	|	Num	|	15
grsinvstincb	|	Gross investment income column b	|	990-PF Pt XIV-3c(4), col (b)	|	Num	|	15
grsinvstincc	|	Gross investment income column c	|	990-PF Pt XIV-3c(4), col (c)	|	Num	|	15
grsinvstincd	|	Gross investment income column d	|	990-PF Pt XIV-3c(4), col (d)	|	Num	|	15
grsinvstinctot	|	Gross investment income total	|	990-PF Pt XIV-3c(4), col (e)	|	Num	|	15
grntapprvfut	|	Grants approved for future payment	|	990-PF Pt XV-3b	|	Num	|	15
progsrvcacold	|	Program service revenue line 1a (excluded)	|	990-PF Pt XVI-A-1a, col (d)	|	Num	|	15
progsrvcacole	|	Program service revenue line 1a (exempt)	|	990-PF Pt XVI-A-1a, col (e)	|	Num	|	15
progsrvcbcold	|	Program service revenue line 1b (excluded)	|	990-PF Pt XVI-A-1b, col (d)	|	Num	|	15
progsrvcbcole	|	Program service revenue line 1b (exempt)	|	990-PF Pt XVI-A-1b, col (e)	|	Num	|	15
progsrvcccold	|	Program service revenue line 1c (excluded)	|	990-PF Pt XVI-A-1c, col (d)	|	Num	|	15
progsrvcccole	|	Program service revenue line 1c (exempt)	|	990-PF Pt XVI-A-1c, col (e)	|	Num	|	15
progsrvcdcold	|	Program service revenue line 1d (excluded)	|	990-PF Pt XVI-A-1d, col (d)	|	Num	|	15
progsrvcdcole	|	Program service revenue line 1d (exempt)	|	990-PF Pt XVI-A-1d, col (e)	|	Num	|	15
progsrvcecold	|	Program service revenue line 1e (excluded)	|	990-PF Pt XVI-A-1e, col (d)	|	Num	|	15
progsrvcecole	|	Program service revenue line 1e (exempt)	|	990-PF Pt XVI-A-1e, col (e)	|	Num	|	15
progsrvcfcold	|	Program service revenue line 1f (excluded)	|	990-PF Pt XVI-A-1f, col (d)	|	Num	|	15
progsrvcfcole	|	Program service revenue line 1f (exempt)	|	990-PF Pt XVI-A-1f, col (e)	|	Num	|	15
progsrvcgcold	|	Program service revenue--fees and contracts from government line 1g (excluded)	|	990-PF Pt XVI-A-1g, col (d)	|	Num	|	15
progsrvcgcole	|	Program service revenue--fees and contracts from government line 1g (exempt)	|	990-PF Pt XVI-A-1g, col (e)	|	Num	|	15
membershpduesd	|	Membership dues and assessments (excluded)	|	990-PF Pt XVI-A-2, col (d)	|	Num	|	15
membershpduese	|	Membership dues and assessments (exempt)	|	990-PF Pt XVI-A-2, col (e)	|	Num	|	15
intonsvngsd	|	Interest on savings and temporary cash investments (excluded)	|	990-PF Pt XVI-A-3, col (d)	|	Num	|	15
intonsvngse	|	Interest on savings and temporary cash investments (exempt)	|	990-PF Pt XVI-A-3, col (e)	|	Num	|	15
dvdndsintd	|	Dividends and interest from securities (excluded)	|	990-PF Pt XVI-A-4, col (d)	|	Num	|	15
dvdndsinte	|	Dividends and interest from securities (exempt)	|	990-PF Pt XVI-A-4, col (e)	|	Num	|	15
trnsfrcashcd	|	Transfer cash to noncharitable exempt organization?	|	990-PF Pt XVII-1a(1)	|	Char	|	1
trnsothasstscd	|	Transfer other assets to noncharitable exempt organization?	|	990-PF Pt XVII-1a(2)	|	Char	|	1
salesasstscd	|	Sale of assets to noncharitable exempt organization?	|	990-PF Pt XVII-1b(1)	|	Char	|	1
prchsasstscd	|	Purchase of assets from noncharitable exempt organization?	|	990-PF Pt XVII-1b(2)	|	Char	|	1
rentlsfacltscd	|	Rental of facilities or other assets?	|	990-PF Pt XVII-1b(3)	|	Char	|	1
reimbrsmntscd	|	Reimbursements arrangements?	|	990-PF Pt XVII-1b(4)	|	Char	|	1
loansguarcd	|	Loans or other guarantees?	|	990-PF Pt XVII-1b(5)	|	Char	|	1
perfservicescd	|	Performance of services or membership or fundraising solicitations?	|	990-PF Pt XVII-1b(6)	|	Char	|	1
sharngasstscd	|	Sharing of facilities, equipment, mailing lists, other assets, or paid employees?	|	990-PF Pt XVII-1c	|	Char	|	1







## CATEGORICAL VARIABLE CODE VALUES




VALUE   |   MEANING
--------|---------------------------
elf	|	
P	|	  Return filed on paper
E	|	  Electronically-filed return
--------|---------------------------
eostatus	|	
1	|	  Unconditional exemption - active
12	|	  Formal exemption not granted (Form 990-PF under IRC 4947(a)(1)) 
--------|---------------------------
miscrev11acd	|	  https://www.census.gov/eos/www/naics/
miscrev11bcd	|	  https://www.census.gov/eos/www/naics/
miscrev11ccd	|	  https://www.census.gov/eos/www/naics/
--------|---------------------------
nonpfrea	|	
00	|	Not reported
01	|	Church
02	|	School (described in 170(b)1)(A)(i))
03	|	Hospital organization (described in 170(b)1)(A)(i))
04	|	Federal, state, or local government unit (described in 170(b)1)(A)(i))
05	|	Medical research organization (described in 170(b)1)(A)(i))
06	|	Organization operated for the benefit of a public college or university (described in 170(b)1)(A)(i))
07	|	Organization that receives a substantial part of its support from government (described in 170(b)1)(A)(i))
08	|	Community trust (described in 170(b)1)(A)(i))
09	|	Section 509(a)(2) organization
11	|	Organization testing for public safety (described in section 509(a)(4))
12	|	Type I Section 509(a)(3) supporting organization
13	|	Type II Section 509(a)(3) supporting organization
14	|	Type III--Functionally integrated Section 509(a)(3) supporting organization
15	|	Type III--Other Section 509(a)(3) supporting organization
--------|---------------------------
operatingcd	|	
Y	|	Operating Foundation
N	|	Nonoperating Foundation
--------|---------------------------
prgmservcode2acd	|	  https://www.census.gov/eos/www/naics/
prgmservcode2bcd	|	  https://www.census.gov/eos/www/naics/
prgmservcode2ccd	|	  https://www.census.gov/eos/www/naics/
prgmservcode2dcd	|	  https://www.census.gov/eos/www/naics/
prgmservcode2ecd	|	  https://www.census.gov/eos/www/naics/
--------|---------------------------
schedbind (Form 990-PF)	|	
Y	|	  Schedule B provided by filer
N	|	  Schedule B not provided by filer
--------|---------------------------
subcd	|	
03	|	  Charitable Corporation
	|	  Educational Organization 
	|	  Literary Organization 
	|	  Organization to Prevent Cruelty to Animals
	|	  Organization to Prevent Cruelty to Children
	|	  Organization for Public Safety Testing
	|	  Religious Organization 
	|	  Scientific Organization 
04	|	  Social welfare organizations
05	|	  Labor and agriculture organizations
06	|	  Business leagues
07	|	  Social and recreation clubs
08	|	  Fraternal beneficiary societies
09	|	  Voluntary employees’ beneficiary associations
10	|	  Domestic fraternal beneficiary societies
11	|	  Teachers' retirement fund associations
12	|	  Benevolent life insurance associations
13	|	  Cemetery companies
14	|	  State-chartered credit unions
15	|	  Mutual insurance companies
16	|	  Corporations organized to finance crop operations
17	|	  Supplemental unemployment compensation trusts
18	|	  Employee-funded pension trusts
19	|	  Veterans’ organizations
20	|	  Group legal services plans
21	|	  Black lung benefit trusts
22	|	  Withdrawal liability payment funds
23	|	  Associations of past and present members of the armed services
24	|	  Trusts (described in section 4049 of ERIS74)
25	|	  Holding companies for pensions and other entities
26	|	  State-sponsored high-risk health insurance plans
27	|	  State-sponsored workers' compensation reinsurance plans
92	|	Section 4947(a)(1) Nonexempt Charitable Trust (Treated as Private Foundation)







## 990PC and 990EZ Version Compatability



```



dat <- read.csv( "https://www.irs.gov/pub/irs-soi/15eofinextract990.dat.dat", sep=" ", skip=1 )

raw.names <- readLines( "https://www.irs.gov/pub/irs-soi/15eofinextract990.dat.dat", n=1 )

dat.names <- strsplit( raw.names, " ")[[1]]

names( dat ) <- dat.names

head( dat )



dat2 <- read.csv( "https://www.irs.gov/pub/irs-soi/15eofinextractEZ.dat", sep=" ", skip=1 )

raw.names <- readLines( "https://www.irs.gov/pub/irs-soi/15eofinextractEZ.dat", n=1 )

dat.names <- strsplit( raw.names, " ")[[1]]

names( dat2 ) <- dat.names

head( dat2 )


> intersect( names(dat), names(dat2) )
 [1] "elf"                  "EIN"                  "subseccd"             "filedf990tcd"        
 [5] "prohibtdtxshltrcd"    "netincfndrsng"        "grsincgaming"         "totassetsend"        
 [9] "totliabend"           "nonpfrea"             "totsupport"           "txrevnuelevied170"   
[13] "srvcsval170"          "pubsuppsubtot170"     "pubsupplesspct170"    "samepubsuppsubtot170"
[17] "grsinc170"            "othrinc170"           "totgftgrntrcvd509"    "txrevnuelevied509"   
[21] "srvcsval509"          "pubsuppsubtot509"     "rcvdfrmdisqualsub509" "subtotpub509"        
[25] "samepubsuppsubtot509" "grsinc509"            "unreltxincls511tx509" "subtotsuppinc509"    
[29] "othrinc509"           "totsupp509"   


> setdiff( names(dat2), names(dat) )
 [1] "a_tax_prd"           "totcntrbs"           "prgmservrev"         "duesassesmnts"      
 [5] "othrinvstinc"        "grsamtsalesastothr"  "basisalesexpnsothr"  "gnsaleofastothr"    
 [9] "grsrevnuefndrsng"    "direxpns"            "grsalesminusret"     "costgoodsold"       
[13] "grsprft"             "othrevnue"           "totrevnue"           "totexpns"           
[17] "totexcessyr"         "othrchgsnetassetfnd" "networthend"         "totnetassetsend"    
[21] "actvtynotprevrptcd"  "chngsinorgcd"        "unrelbusincd"        "contractioncd"      
[25] "politicalexpend"     "filedfYYN0polcd"     "loanstoofficerscd"   "loanstoofficers"    
[29] "initiationfee"       "grspublicrcpts"      "s4958excessbenefcd"  "totnoforgscnt"      
[33] "gftgrntrcvd170"      "excds2pct170"        "netincunrelatd170"   "totsupport170"      
[37] "grsrcptsrelatd170"   "grsrcptsadmiss509"   "grsrcptsactvts509"   "excds1pct509"       
[41] "pubsupplesssub509"   "netincunreltd509"   


> setdiff( names(dat), names(dat2) )
  [1] "tax_prd"               "s50Yc3or4947aYcd"      "schdbind"              "politicalactvtscd"    
  [5] "lbbyingactvtscd"       "subjto6033cd"          "dnradvisedfundscd"     "prptyintrcvdcd"       
  [9] "maintwrkofartcd"       "crcounselingqstncd"    "hldassetsintermpermcd" "rptlndbldgeqptcd"     
 [13] "rptinvstothsecd"       "rptinvstprgrelcd"      "rptothasstcd"          "rptothliabcd"         
 [17] "sepcnsldtfinstmtcd"    "sepindaudfinstmtcd"    "inclinfinstmtcd"       "operateschoolsY70cd"  
 [21] "frgnofficecd"          "frgnrevexpnscd"        "frgngrntscd"           "frgnaggragrntscd"     
 [25] "rptprofndrsngfeescd"   "rptincfnndrsngcd"      "rptincgamingcd"        "operatehosptlcd"      
 [29] "hospaudfinstmtcd"      "rptgrntstogovtcd"      "rptgrntstoindvcd"      "rptyestocompnstncd"   
 [33] "txexmptbndcd"          "invstproceedscd"       "maintescrwaccntcd"     "actonbehalfcd"        
 [37] "engageexcessbnftcd"    "awarexcessbnftcd"      "loantofficercd"        "grantoofficercd"      
 [41] "dirbusnreltdcd"        "fmlybusnreltdcd"       "servasofficercd"       "recvnoncashcd"        
 [45] "recvartcd"             "ceaseoperationscd"     "sellorexchcd"          "ownsepentcd"          
 [49] "reltdorgcd"            "intincntrlcd"          "orgtrnsfrcd"           "conduct5percentcd"    
 [53] "compltschocd"          "f1096cnt"              "fw2gcnt"               "wthldngrulescd"       
 [57] "noemplyeesw3cnt"       "filerqrdrtnscd"        "unrelbusinccd"         "frgnacctcd"           
 [61] "prtynotifyorgcd"       "filedf8886tcd"         "solicitcntrbcd"        "exprstmntcd"          
 [65] "providegoodscd"        "notfydnrvalcd"         "filedf8N8Ncd"          "f8282cnt"             
 [69] "fndsrcvdcd"            "premiumspaidcd"        "filedf8899cd"          "filedfY098ccd"        
 [73] "excbushldngscd"        "s4966distribcd"        "distribtodonorcd"      "initiationfees"       
 [77] "grsrcptspublicuse"     "grsincmembers"         "grsincother"           "filedlieufY04Ycd"     
 [81] "txexmptint"            "qualhlthplncd"         "qualhlthreqmntn"       "qualhlthonhnd"        
 [85] "rcvdpdtngcd"           "filedf7N0cd"           "totreprtabled"         "totcomprelatede"      
 [89] "totestcompf"           "noindiv100kcnt"        "nocontractor100kcnt"   "totcntrbgfts"         
 [93] "prgmservcode2acd"      "totrev2acola"          "prgmservcode2bcd"      "totrev2bcola"         
 [97] "prgmservcode2ccd"      "totrev2ccola"          "prgmservcode2dcd"      "totrev2dcola"         
[101] "prgmservcode2ecd"      "totrev2ecola"          "totrev2fcola"          "totprgmrevnue"        
[105] "invstmntinc"           "txexmptbndsproceeds"   "royaltsinc"            "grsrntsreal"          
[109] "grsrntsprsnl"          "rntlexpnsreal"         "rntlexpnsprsnl"        "rntlincreal"          
[113] "rntlincprsnl"          "netrntlinc"            "grsalesecur"           "grsalesothr"          
[117] "cstbasisecur"          "cstbasisothr"          "gnlsecur"              "gnlsothr"             
[121] "netgnls"               "grsincfndrsng"         "lessdirfndrsng"        "lessdirgaming"        
[125] "netincgaming"          "grsalesinvent"         "lesscstofgoods"        "netincsales"          
[129] "miscrev11acd"          "miscrevtota"           "miscrev11bcd"          "miscrevtot11b"        
[133] "miscrev11ccd"          "miscrevtot11c"         "miscrevtot11d"         "miscrevtot11e"        
[137] "totrevenue"            "grntstogovt"           "grnsttoindiv"          "grntstofrgngovt"      
[141] "benifitsmembrs"        "compnsatncurrofcr"     "compnsatnandothr"      "othrsalwages"         
[145] "pensionplancontrb"     "othremplyeebenef"      "payrolltx"             "feesforsrvcmgmt"      
[149] "legalfees"             "accntingfees"          "feesforsrvclobby"      "profndraising"        
[153] "feesforsrvcinvstmgmt"  "feesforsrvcothr"       "advrtpromo"            "officexpns"           
[157] "infotech"              "royaltsexpns"          "occupancy"             "travel"               
[161] "travelofpublicoffcl"   "converconventmtng"     "interestamt"           "pymtoaffiliates"      
[165] "deprcatndepletn"       "insurance"             "othrexpnsa"            "othrexpnsb"           
[169] "othrexpnsc"            "othrexpnsd"            "othrexpnse"            "othrexpnsf"           
[173] "totfuncexpns"          "nonintcashend"         "svngstempinvend"       "pldgegrntrcvblend"    
[177] "accntsrcvblend"        "currfrmrcvblend"       "rcvbldisqualend"       "notesloansrcvblend"   
[181] "invntriesalesend"      "prepaidexpnsend"       "lndbldgsequipend"      "invstmntsend"         
[185] "invstmntsothrend"      "invstmntsprgmend"      "intangibleassetsend"   "othrassetsend"        
[189] "accntspayableend"      "grntspayableend"       "deferedrevnuend"       "txexmptbndsend"       
[193] "escrwaccntliabend"     "paybletoffcrsend"      "secrdmrtgsend"         "unsecurednotesend"    
[197] "othrliabend"           "unrstrctnetasstsend"   "temprstrctnetasstsend" "permrstrctnetasstsend"
[201] "capitalstktrstend"     "paidinsurplusend"      "retainedearnend"       "totnetassetend"       
[205] "totnetliabastend"      "totnooforgscnt"        "gftgrntsrcvd170"       "exceeds2pct170"       
[209] "netincunreltd170"      "totsupp170"            "grsrcptsrelated170"    "grsrcptsadmissn509"   
[213] "grsrcptsactivities509" "exceeds1pct509"        "pubsupplesub509"       "netincunrelatd509" 

```



## SAMPLE CODE FOR DOWNLOADING ZIPPED FILES


```r


dat <- read.csv( "https://www.irs.gov/pub/irs-soi/15eofinextractEZ.dat", sep=" ", skip=1 )

raw.names <- readLines( "https://www.irs.gov/pub/irs-soi/15eofinextractEZ.dat", n=1 )

n2 <- strsplit( raw.names, " ")[[1]]

names( dat ) <- n2

head( dat )



setwd( "C:/Users/jdlecy/Downloads/14eofinextract990ez" )



dat <- read.csv( "py14_EZ.dat", sep=" ", skip=1 )

raw.names <- readLines( "py14_EZ.dat", n=1 )

n1 <- strsplit( raw.names, " ")[[1]]

names( dat ) <- dat.names

head( dat )

setdiff( union(n1,n2), intersect(n1,n2) )





# download and unzip

file.url <- "https://apps.irs.gov/pub/epostcard/data-download-epostcard.zip"

download.file( url=file.url, "epostcard.zip" )

unzip( "epostcard.zip" )

file.remove( "epostcard.zip" )

dat.990n <- read.delim( file="data-download-epostcard.txt", 
            header = FALSE, 
            sep = "|", 
            quote = "",
            dec = ".", 
            fill = TRUE,  
            colClasses="character"
          )


```
