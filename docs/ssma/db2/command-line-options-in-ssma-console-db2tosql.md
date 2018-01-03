---
title: "SSMA 主控台 (DB2ToSQL) 中的命令列選項 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 237354e9-25c4-4386-9d1f-ca0618d4a9a0
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d5eff60694cdcfdb4d2d147ae0531fbbc2ecfb32
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="command-line-options-in-ssma-console-db2tosql"></a>SSMA 主控台 (DB2ToSQL) 中的命令列選項
Microsoft 為您提供執行及控制 SSMA 活動組強固命令列選項。 這可確保各節詳細說明相同。  
  
## <a name="command-line-options-in-ssma-console"></a>SSMA 主控台中的命令列選項  
此處所述是主控台命令的選項。  
  
本節中，為了 'option' 一詞也稱為 'switch'。  
  
選項不區分大小寫，並開始使用 '**-**'或，'**/**' 字元。  
  
如果指定了選項，它會成為強制指定對應的選項參數。  
  
選項參數必須以空格分隔從選項字元。  
  
**語法範例：**  
  
`C:\> SSMAforDB2Console.EXE -s scriptfile`  
  
`C:\> SSMAforDB2Console.EXE -s “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \AssessmentReportGenerationSample.xml” –v “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \VariableValueFileSample.xml” –c “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ServersConnectionFileSample.xml”`  
  
包含空格的資料夾或檔案名稱應指定雙引號括住。  
  
命令列項目和錯誤訊息的輸出會儲存在 STDOUT 或指定的檔案。  
  
### <a name="script-file-option-sscript"></a>指令碼檔案的選項:-s/指令碼  
必要的參數，指令碼檔案路徑/名稱指定要執行之 SSMA 的命令順序的指令碼。  
  
**語法範例：**  
  
`C:\>SSMAforDB2Console.EXE –s “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>變數值的 File 選項:-v/變數  
這個檔案包含在指令碼檔案中使用變數。 這是選用參數。 如果您沒有變數檔案中宣告變數並用於指令碼檔案中，應用程式會產生錯誤並結束主控台執行。  
  
**語法範例：**  
  
-   在多個變數值檔案，可能是其中一個預設值，而另一個執行個體特定值時適用中定義的變數。 最後一個命令列引數中指定的變數檔接受喜好設定，以防重複的變數：  
  
    `C:\>SSMAforDB2Console.EXE -s`  
  
    `“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>– C/serverconnection 伺服器連接檔案的選項：  
此檔案包含每一部伺服器的伺服器連接資訊。 識別每個伺服器定義唯一的伺服器識別碼。 連接的指令碼檔案中所參考的伺服器識別碼相關命令。  
  
定義伺服器可以是伺服器連接檔案及/或指令碼檔案的一部分。 指令碼檔案中的伺服器識別碼的優先順序高於伺服器連接檔案，以防重複的伺服器識別碼。  
  
**語法範例：**  
  
-   伺服器識別碼會以指令碼檔案且其定義在不同的伺服器連接檔案中，伺服器連接檔案會使用變數值檔案中定義的變數：  
  
    `C:\>SSMAforDB2Console.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   指令碼檔案中內嵌的伺服器定義：  
  
    `C:\>SSMAforDB2Console.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 輸出選項:-x / xmloutput [xmloutputfile]  
此命令用來輸出至主控台或至 xml 檔案的 xml 格式的命令輸出訊息。  
  
有兩個選項可用來 xmloutput，viz。。，：  
  
-   如果 xmloutput 切換之後提供的檔案路徑，則檔案會重新導向輸出。  
  
    **語法範例：**  
  
    `C:\>SSMAforDB2Console.EXE –s`  
  
    `“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   如果沒有 filepath 提供 xmloutput 切換之後 xmlout 會顯示在本身的主控台。  
  
    **語法範例：**  
  
    `C:\>SSMAforDB2Console.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>記錄檔選項: – l/記錄檔  
主控台應用程式中的所有 SSMA 作業取得都記錄在記錄檔中。 這是選用參數。 如果在命令列指定記錄檔和它的路徑，取得指定的位置中產生的記錄。 否則，它取得產生的預設位置。  
  
**語法範例：**  
  
`C:\>SSMAforDB2Console.EXE`  
  
`“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>– E/projectenvironment 專案環境資料夾的選項：  
這表示目前的 SSMA 專案的專案的環境設定資料夾。 這個參數是選擇性的。  
  
**語法範例：**  
  
`C:\>SSMAforDB2Console.EXE –s`  
  
`“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option-psecurepassword"></a>– P/securepassword 安全密碼的選項：  
這個選項表示伺服器連接的加密的密碼。 不同於其他所有選項： 選項或都不執行任何指令碼中任何移轉相關的活動可幫助，但可協助管理移轉專案中使用的伺服器連接的密碼加密。  
  
您不能輸入命令列參數選項或密碼。 否則，它會導致錯誤。 如需詳細資訊，請參閱[管理密碼](http://msdn.microsoft.com/en-us/56d546e3-8747-4169-aace-693302667e94)> 一節。  
  
支援下列子選項`–p/securepassword`:  
  
-   若要將密碼以保護儲存體，針對指定的伺服器識別碼或伺服器的連接檔案中定義的所有伺服器識別碼。 -Overwrite 選項，以下更新密碼，如果已經存在：  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   若要從受保護的儲存體指定的伺服器識別碼或所有的伺服器識別碼移除加密的密碼：  
  
    `–p/securepassword –r/remove {<server_id> [, …n] | all}`  
  
-   若要顯示為其密碼已經加密的伺服器識別碼的清單：  
  
    `–p/securepassword –l/list`  
  
-   若要匯出的密碼儲存在受保護的儲存體加密的檔案。 這個檔案是以使用者指定的密碼片語加密。  
  
    `–p/securepassword –e/export {<server-id> [, …n] | all} <encrypted-password -file>`  
  
-   加密-稍早匯出檔案匯入到本機受保護的儲存體使用使用者指定的密碼片語。 一旦進行解密檔案時，它會儲存在新的檔案，接著是本機電腦上進行加密。  
  
    `–p/securepassword –i/import {<server-id> [, …n] | all} <encrypted-password -file>`  
  
    可以使用逗點分隔符號來指定多個伺服器識別碼。  
  
### <a name="help-option-help"></a>說明選項:-？ / 說明  
會顯示 SSMA 主控台選項的語法摘要：  
  
`C:\>SSMAforDB2Console.EXE -?`  
  
SSMA 主控台命令列選項表格式顯示中，請參閱[附錄-1 &#40; DB2ToSQL &#41;](../../ssma/db2/appendix-1-db2tosql.md)。  
  
### <a name="securepassword-help-option-securepassword--help"></a>SecurePassword 說明選項:-securepassword-？ / 說明  
會顯示 SSMA 主控台選項的語法摘要：  
  
`C:\>SSMAforDB2Console.EXE -securepassword -?`  
  
SSMA 主控台命令列選項表格式顯示中，請參閱[附錄-1 &#40; DB2ToSQL &#41;](../../ssma/db2/appendix-1-db2tosql.md)  
  
### <a name="next-step"></a>下一個步驟  
下一個步驟取決於您的專案需求：  
  
1.  指定的密碼或匯出 / 匯入的密碼，請參閱[管理密碼 &#40; DB2ToSQL &#41;](../../ssma/db2/managing-passwords-db2tosql.md)。  
  
2.  產生報告，請參閱[產生報表 &#40; DB2ToSQL &#41;](../../ssma/db2/generating-reports-db2tosql.md)。  
  
3.  如需疑難排解主控台中的問題，請參閱[疑難排解 &#40; DB2ToSQL &#41;](../../ssma/db2/troubleshooting-db2tosql.md)。  
  
