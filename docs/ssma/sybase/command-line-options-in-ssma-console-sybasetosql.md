---
title: SSMA 主控台 (SybaseToSQL) 中的命令列選項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Command Line Options
ms.assetid: 337cbd26-67b7-4c88-9deb-d0a69a3d7714
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 62c56e876a3579d136eb2bff7a594d651b4e084e
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392565"
---
# <a name="command-line-options-in-ssma-console-sybasetosql"></a>SSMA 主控台中的命令列選項 (SybaseToSQL)
Microsoft 為您提供一組強大的命令列選項來執行，並控制 SSMA 活動。 後續章節將詳細說明相同。  
  
## <a name="command-line-options-in-ssma-console"></a>SSMA 主控台中的命令列選項  
此處所述是主控台命令的選項。  
  
本節中，為了 「 選項 」 一詞也稱為 'switch'。  
  
-   選項不區分大小寫和可能的開頭是 '**-**'**/**' 字元。  
  
-   如果指定了選項，就一定要指定對應的選項參數。  
  
-   選項參數必須以泛空白字元分隔從選項中的字元。  
  
    **語法範例：**  
  
    `C:\> SSMAforSybaseConsole.EXE -s scriptfile`  
  
    `C:\> SSMAforSybaseConsole.EXE -s “C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\AssessmentReportGenerationSample.xml” –v “C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\VariableValueFileSample.xml” –c “C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ServersConnectionFileSample.xml”`  
  
-   包含空格的資料夾或檔案名稱應指定雙引號括住。  
  
-   命令列項目和錯誤訊息的輸出會儲存在 STDOUT 或指定的檔案。  
  
### <a name="script-file-option-sscript"></a>指令碼檔案的選項:-s/指令碼  
必要的參數，指令碼檔案的路徑/名稱指定要由 SSMA 執行的命令順序的指令碼。  
  
**語法範例：**  
  
`C:\>SSMAforSybaseConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>變數值檔案的選項: – v/變數  
此檔案包含在指令碼檔案中使用的變數。 這是選用參數。 如果變數不是變數的檔案中宣告，並使用指令碼檔案中，應用程式就會產生錯誤，並結束主控台執行。  
  
**語法範例：**  
  
-   定義多個變數值檔案，可能是一個預設值，另一個執行個體特定值時適用的變數。 最後一個命令列引數中指定的變數檔案會接受喜好設定，以防萬一發生重複的變數：  
  
    `C:\>SSMAforSybaseConsole.EXE -s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>伺服器連接檔案的選項:-c/serverconnection  
此檔案包含每一部伺服器的伺服器連接資訊。 每個伺服器定義會識別唯一的伺服器識別碼。 連接的指令碼檔案中所參考的伺服器識別碼與命令相關。  
  
伺服器定義可以是伺服器連線檔案和/或指令碼檔案的一部分。 指令碼檔案中的伺服器識別碼的優先順序高於伺服器連線檔案中，如果有重複的伺服器識別碼。  
  
**語法範例：**  
  
-   伺服器識別碼之指令檔中且定義不同的伺服器連線檔案中，伺服器連線檔案會使用變數值檔案中定義的變數：  
  
    `C:\>SSMAforSybaseConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   伺服器定義內嵌在指令碼檔案中：  
  
    `C:\>SSMAforSybaseConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 輸出選項:-x / xmloutput [xmloutputfile]  
此命令用來輸出至主控台或至 xml 檔案的 xml 格式的命令輸出訊息。  
  
有兩個選項可供 xmloutput， 報導..,：  
  
-   如果 xmloutput 切換之後提供檔案路徑，則會輸出重新導向至檔案。  
  
    **語法範例：**  
  
    `C:\>SSMAforSybaseConsole.EXE –s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   如果沒有檔案路徑會提供 xmloutput 切換之後 xmlout 會顯示在主控台本身。  
  
    **語法範例：**  
  
    `C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>記錄檔選項:-l/記錄檔  
在主控台應用程式中的所有 SSMA 作業取得都記錄在記錄檔。 這是選用參數。 如果在命令列指定記錄檔和其路徑，取得產生記錄檔，在指定的位置。 否則，它會產生在其預設位置。  
  
**語法範例：**  
  
`C:\>SSMAforSybaseConsole.EXE`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>專案環境資料夾的選項:-e/projectenvironment  
這表示目前的 SSMA 專案的專案環境設定 資料夾。 這個參數是選擇性的。  
  
**語法範例：**  
  
`C:\>SSMAforSybaseConsole.EXE –s`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option-psecurepassword"></a>安全的密碼選項:-p/securepassword  
這個選項表示伺服器連接的加密的密碼。 不同於其他所有選項： 選項或都不會執行任何指令碼有助於移轉相關的任何活動，但可協助管理移轉專案中使用的伺服器連接的密碼加密。  
  
您無法輸入任何其他選項和密碼，做為命令列參數。 否則，它會導致錯誤。 如需詳細資訊，請參閱[管理密碼](managing-passwords-sybasetosql.md)一節。  
  
支援下列子選項`–p/securepassword`:  
  
-   若要將密碼保護的儲存體指定的伺服器識別碼，或在伺服器連線檔案中定義的所有伺服器 id。 -Overwrite 選項下, 面，更新密碼，如果已經存在：  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   若要從受保護的儲存體指定的伺服器識別碼或所有的伺服器識別碼移除加密的密碼：  
  
    `–p/securepassword –r/remove {<server_id> [, …n] | all}`  
  
-   若要顯示的加密密碼的伺服器識別碼的清單：  
  
    `–p/securepassword –l/list`  
  
-   若要匯出受保護的儲存體加密的檔案中儲存的密碼。 這個檔案是以使用者指定的複雜密碼加密。  
  
    `–p/securepassword –e/export {<server-id> [, …n] | all} <encrypted-password -file>`  
  
-   加密-稍早匯出檔案匯入本機受保護的儲存體，使用使用者指定的複雜密碼。 一旦解密檔案，它會儲存在新的檔案，接著，在本機電腦上加密。  
  
    `–p/securepassword –i/import {<server-id> [, …n] | all} <encrypted-password -file>`  
  
    可以使用逗號分隔符號來指定多個伺服器識別碼。  
  
### <a name="help-option-help"></a>[說明] 選項:-？ / 協助  
顯示 SSMA 主控台選項的語法的摘要：  
  
`C:\>SSMAforSybaseConsole.EXE -?`  
  
SSMA 主控台命令列選項以表格形式顯示，請參閱[附錄-1 &#40;SybaseToSQL&#41;](../../ssma/sybase/appendix-1-sybasetosql.md)。  
  
### <a name="securepassword-help-option-securepassword--help"></a>SecurePassword 說明選項:-securepassword-？ / 協助  
顯示 SSMA 主控台選項的語法的摘要：  
  
`C:\>SSMAforSybaseConsole.EXE -securepassword -?`  
  
SSMA 主控台命令列選項以表格形式顯示，請參閱[附錄-1 &#40;SybaseToSQL&#41;](../../ssma/sybase/appendix-1-sybasetosql.md)  
  
### <a name="next-step"></a>下一個步驟  
下一個步驟取決於您的專案需求：  
  
-   指定的密碼或匯出 / 匯入的密碼，請參閱 <<c0> [ 管理的密碼&#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md)。</c0>  
  
-   要產生報表，請參閱[產生的報表&#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)。  
  
-   如需疑難排解主控台中的問題，請參閱[疑難排解&#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md)。  
  
