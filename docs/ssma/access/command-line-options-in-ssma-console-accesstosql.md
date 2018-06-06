---
title: SSMA 主控台 (AccessToSQL) 中的命令列選項 |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
ms.custom: ''
ms.date: 08/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 361ef1f9fcac31f864350098a2c3d223c59e2afe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>SSMA 主控台 (AccessToSQL) 中的命令列選項
Microsoft 提供一組強固的執行及控制 SSMA 活動的命令列選項。 後續章節將提供其他詳細資料。  
  
## <a name="command-line-options-in-the-ssma-console"></a>SSMA 主控台中的命令列選項  
此處所述是主控台命令的選項。  
  
本節中，為了 'option' 一詞也稱為 'switch'。  
  
選項不區分大小寫，並開始使用 '**-**'**/**' 字元。  
  
如果指定了選項，它是強制性，您會指定對應的選項參數。  
  
選項參數必須以空格分隔從選項字元。  
  
**語法範例：**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml” –v “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml” –c “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml”`  
  
包含空格的資料夾或檔案名稱應指定雙引號括住。  
  
命令列的項目和錯誤訊息的輸出會儲存在 STDOUT 或指定的檔案。  
  
### <a name="script-file-option-sscript"></a>指令碼檔案的選項:-s/指令碼  
必要的參數，指令碼檔案路徑/名稱指定要執行之 SSMA 的命令順序的指令碼。  
  
**語法範例：**  
  
`C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>變數值 file 選項:-v/變數  
變數值檔案包含在指令碼檔案中使用變數。 這個參數是選擇性的。 如果您沒有變數檔案中宣告變數並用於指令碼檔案中，應用程式會產生錯誤並結束主控台執行。  
  
**語法範例：**  
  
-   在多個變數值檔案，可能是其中一個預設值，而另一個具有特定執行個體的值時適用中定義的變數。 最後一個命令列引數中指定的變數檔接受喜好設定，以防重複的變數：  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>伺服器連接檔案的選項: – c/serverconnection  
此檔案包含每一部伺服器的伺服器連接資訊。 識別每個伺服器定義唯一的伺服器識別碼。 伺服器識別碼會參考連接相關的命令的指令碼檔案中。  
  
定義伺服器可以是伺服器連接檔案及/或指令碼檔案的一部分。 指令碼檔案中的伺服器識別碼的優先順序高於伺服器連接檔案，以防重複的伺服器識別碼。  
  
**語法範例：**  
  
-   伺服器識別碼可用在指令碼檔案。 它們是不同的伺服器連接檔案中定義。 這個檔案會使用變數值檔案中所定義的變數：  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   指令碼檔案中內嵌的伺服器定義：  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 輸出選項:-x / xmloutput [xmloutputfile]  
此命令用來輸出至主控台或至 xml 檔案的 xml 格式的命令輸出訊息。  
  
有兩個選項可供 xmloutput，也就是：  
  
-   如果提供 filepath xmloutput 切換之後，檔案會重新導向輸出。  
  
    **語法範例：**  
  
    `C:\>SSMAforAccessConsole.EXE –s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   如果沒有 filepath 提供 xmloutput 切換之後，則會顯示 xmlout 本身在主控台上。  
  
    **語法範例：**  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>記錄檔選項: – l/記錄檔  
主控台應用程式中的所有 SSMA 作業都會都記錄在記錄檔，以及參數是選擇性的。 如果在命令列指定記錄檔和它的路徑，取得指定的位置中產生的記錄。 否則，它取得產生的預設位置。  
  
**語法範例：**  
  
`C:\>SSMAforAccessConsole.EXE`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>專案環境資料夾選項:-e/projectenvironment  
這個選擇性參數代表目前的 SSMA 專案的專案的環境設定資料夾。  
  
**語法範例：**  
  
`C:\>SSMAforAccessConsole.EXE –s`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
||  
|-|  
||  
  
### <a name="secure-password-option-psecurepassword"></a>安全密碼的選項: – p/securepassword  
這個選項表示伺服器連接的加密的密碼。 它會與所有其他選項，但不執行任何指令碼或任何移轉相關的活動，在協助有助於管理在移轉專案中使用的伺服器連接的密碼加密的。  
  
您不能輸入命令列參數選項或密碼。 否則，它會導致錯誤。 如需詳細資訊，請參閱[管理密碼](http://msdn.microsoft.com/b099d0f9-dd37-4c87-8b6f-ed0177881ea4)> 一節。  
  
支援下列 suboptions `–p/securepassword`:  
  
-   若要加入密碼，或更新現有的密碼，為受保護的存放裝置指定的伺服器識別碼，或伺服器的連接檔案中定義的所有伺服器識別碼：  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
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
  
### <a name="help-option-help"></a>Help 選項:-？ / 說明  
會顯示 SSMA 主控台選項的語法摘要：  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
SSMA 主控台命令列選項表格式顯示中，請參閱[附錄-1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)。  
  
### <a name="securepassword-help-option-securepassword--help"></a>SecurePassword 說明選項:-securepassword-？ / 說明  
會顯示 SSMA 主控台選項的語法摘要：  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
SSMA 主控台命令列選項表格式顯示中，請參閱[附錄-1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>後續的步驟  
下一個步驟取決於您的專案需求：  
  
1.  指定的密碼或匯出 / 匯入的密碼，請參閱[管理密碼&#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md)。  
  
2.  產生報告，請參閱[產生報表&#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)。  
  
3.  如需疑難排解主控台中的問題，請參閱[疑難排解&#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md)。  
  
