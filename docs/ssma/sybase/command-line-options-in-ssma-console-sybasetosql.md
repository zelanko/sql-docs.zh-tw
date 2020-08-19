---
description: SSMA 主控台中的命令列選項 (SybaseToSQL)
title: SSMA 主控台中的命令列選項 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Command Line Options
ms.assetid: 337cbd26-67b7-4c88-9deb-d0a69a3d7714
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1c987294c92dfcd5a7577f96ad5d77c9e27f975b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468780"
---
# <a name="command-line-options-in-ssma-console-sybasetosql"></a>SSMA 主控台中的命令列選項 (SybaseToSQL)
Microsoft 為您提供一組健全的命令列選項，以執行和控制 SSMA 活動。 後續各節會詳細說明相同的。  
  
## <a name="command-line-options-in-ssma-console"></a>SSMA 主控台中的命令列選項  
此處說明的是主控台命令選項。  
  
基於本節的目的，「選項」一詞也稱為「參數」。  
  
-   選項不區分大小寫，且開頭可能是 ' **-** ' 或 ' ' **/** 字元。  
  
-   如果指定了選項，就必須指定對應的選項參數。  
  
-   選項參數必須以空白字元區隔的選項。  
  
    **語法範例：**  
  
    `C:\> SSMAforSybaseConsole.EXE -s scriptfile`  
  
    `C:\> SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\VariableValueFileSample.xml" -c "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ServersConnectionFileSample.xml"`  
  
-   包含空格的資料夾或檔案名應以雙引號來指定。  
  
-   命令列專案和錯誤訊息的輸出會儲存在 STDOUT 或指定的檔案中。  
  
### <a name="script-file-option--sscript"></a>指令檔選項：-s/腳本  
強制參數，腳本檔案路徑/名稱會指定 SSMA 要執行之命令順序的腳本。  
  
**語法範例：**  
  
`C:\>SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="variable-value-file-option--vvariable"></a>變數值檔案選項：-v/variable  
此檔案包含在腳本檔案中使用的變數。 這是選擇性參數。 如果變數未在變數檔案中宣告，並且在腳本檔案中使用，則應用程式會產生錯誤並結束主控台執行。  
  
**語法範例：**  
  
-   在多個變數值檔案中定義的變數，可能是具有預設值的變數，而另一個則是具有實例特定值（如果適用）。 在命令列引數中指定的最後一個變數檔案會採用喜好設定，以防變數重複：  
  
    `C:\>SSMAforSybaseConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml" -v c:\migration`  
  
    `projects\global_variablevaluefile.xml -v "c:\migrationprojects\instance_variablevaluefile.xml"`  
  
### <a name="server-connection-file-option--cserverconnection"></a>伺服器連接檔案選項：-c/serverconnection  
此檔案包含每部伺服器的伺服器連接資訊。 每個伺服器定義都是由唯一的伺服器識別碼來識別。 腳本檔案中會參考伺服器識別碼以取得連接相關的命令。  
  
伺服器定義可以是伺服器連接檔案和/或腳本檔案的一部分。 腳本檔案中的伺服器識別碼優先于伺服器連接檔案，以防伺服器識別碼重複。  
  
**語法範例：**  
  
-   伺服器識別碼會用於腳本檔中，而且會在個別的伺服器連接檔案中定義，而伺服器連接檔會使用變數值檔案中所定義的變數：  
  
    `C:\>SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -v`  
  
    `c:\SsmaProjects\myvaluefile1.xml -c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   伺服器定義內嵌在腳本檔案中：  
  
    `C:\>SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 輸出選項：-x/xmloutput [xmloutputfile]  
此命令可用來將 xml 格式的命令輸出訊息輸出至主控台或 xml 檔案。  
  
有兩個選項可供 xmloutput、視覺效果：  
  
-   如果在 xmloutput 參數之後提供檔案路徑，則會將輸出重新導向至檔案。  
  
    **語法範例：**  
  
    `C:\>SSMAforSybaseConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -x d:\xmloutput\project1output.xml`  
  
-   如果 xmloutput 參數之後未提供任何 filepath，則 xmlout 會顯示在主控台本身。  
  
    **語法範例：**  
  
    `C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -xmloutput`  
  
### <a name="log-file-option--llog"></a>記錄檔選項：-l/log  
主控台應用程式中的所有 SSMA 作業都會記錄在記錄檔中。 這是選擇性參數。 如果在命令列指定了記錄檔及其路徑，則會在指定的位置產生記錄檔。 否則，它會在其預設位置產生。  
  
**語法範例：**  
  
`C:\>SSMAforSybaseConsole.EXE`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option--eprojectenvironment"></a>專案環境資料夾選項：-e/projectenvironment  
這表示目前 SSMA 專案的 [專案環境設定] 資料夾。 這個參數是選擇性的。  
  
**語法範例：**  
  
`C:\>SSMAforSybaseConsole.EXE -s`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option--psecurepassword"></a>安全密碼選項：-p/securepassword  
此選項表示伺服器連接的加密密碼。 它與所有其他選項不同：選項不會執行任何腳本，也不會在任何遷移相關的活動中有所説明，但有助於管理用於遷移專案的伺服器連接的密碼加密。  
  
您無法將任何其他選項或密碼輸入為命令列參數。 否則會產生錯誤。 如需詳細資訊，請參閱 [管理密碼](managing-passwords-sybasetosql.md) 一節。  
  
以下是支援的子選項 `-p/securepassword` ：  
  
-   針對指定的伺服器識別碼或伺服器連接檔中定義的所有伺服器識別碼，將密碼新增至受保護的存放裝置。 以下的-overwrite 選項會更新密碼（如果已存在）：  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   若要從指定之伺服器識別碼或所有伺服器識別碼的受保護儲存區中移除加密的密碼：  
  
    `-p/securepassword -r/remove {<server_id> [, ...n] | all}`  
  
-   若要顯示加密密碼的伺服器識別碼清單：  
  
    `-p/securepassword -l/list`  
  
-   將儲存在受保護儲存體中的密碼匯出至加密的檔案。 此檔案會使用使用者指定的傳遞片語進行加密。  
  
    `-p/securepassword -e/export {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
-   先前匯出的加密檔案會使用使用者指定的傳遞片語匯入本機受保護的儲存體。 檔案解密之後，會儲存在新的檔案中，然後在本機電腦上進行加密。  
  
    `-p/securepassword -i/import {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
    您可以使用逗號分隔來指定多個伺服器識別碼。  
  
### <a name="help-option--help"></a>Help 選項：-？/Help  
顯示 SSMA 主控台選項的語法摘要：  
  
`C:\>SSMAforSybaseConsole.EXE -?`  
  
如需 SSMA 主控台命令列選項的表格式顯示，請參閱 [附錄-1 &#40;SybaseToSQL&#41;](../../ssma/sybase/appendix-1-sybasetosql.md)。  
  
### <a name="securepassword-help-option--securepassword--help"></a>SecurePassword Help 選項：-SecurePassword-？/Help  
顯示 SSMA 主控台選項的語法摘要：  
  
`C:\>SSMAforSybaseConsole.EXE -securepassword -?`  
  
如需 SSMA 主控台命令列選項的表格式顯示，請參閱 [附錄-1 &#40;SybaseToSQL&#41;](../../ssma/sybase/appendix-1-sybasetosql.md)  
  
### <a name="next-step"></a>後續步驟  
下一步取決於您的專案需求：  
  
-   如需指定密碼或匯出/匯入密碼，請參閱 [管理密碼 &#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md)。  
  
-   若要產生報表，請參閱 [&#40;SybaseToSQL&#41;產生報表 ](../../ssma/sybase/generating-reports-sybasetosql.md)。  
  
-   如需疑難排解主控台中的問題，請參閱 [&#40;SybaseToSQL&#41;的疑難排解 ](../../ssma/sybase/troubleshooting-sybasetosql.md)。  
  
