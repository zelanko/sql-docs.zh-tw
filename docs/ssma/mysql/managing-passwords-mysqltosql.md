---
title: 管理密碼 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Password management, importing or exporting encrypted password
- Password management, securing password
ms.assetid: 4ffbc587-ea3f-49ad-bc42-a654f672325e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f04b786aaef8a994cff1051a289bbdad3b3fd5ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311965"
---
# <a name="managing-passwords-mysqltosql"></a>管理密碼 (MySQLToSQL)
本章節是關於保護資料庫的密碼和匯入，或將它們匯出到伺服器的程序：  
  
1.  保護密碼  
  
2.  匯出或匯入加密的密碼  
  
## <a name="securing-password"></a>保護密碼  
SSMA 可讓您保護您的資料庫的密碼。  
  
您可以使用下列程序來實作安全的連線：  
  
指定有效的密碼，使用下列三種方法之一：  
  
1.  **純文字格式：** 在 [密碼] 節點的值屬性中輸入資料庫密碼。 在指令碼檔案或伺服器連線檔案伺服器一節中的伺服器定義節點底下找到。  
  
    以純文字密碼並不安全的。 因此，您將會遇到下列警告訊息中的主控台輸出：*「 伺服器&lt;伺服器識別碼&gt;密碼會提供不安全的純文字形式 SSMA 主控台應用程式會提供一個選項來保護透過加密的密碼，SSMA 說明檔中的-securepassword 選項，如需詳細資訊，請參閱資訊 」。*  
  
    **加密的密碼：** 指定的密碼，在此情況下，是以加密形式儲存 ProtectedStorage.ssma 在本機電腦上。  
  
    -   **保護密碼**  
  
        -   執行`SSMAforMySQLConsole.exe`與`-securepassword`，並在命令列傳遞伺服器包含伺服器定義一節中的 [密碼] 節點的連接或指令碼檔案中新增參數。  
  
        -   在提示字元中輸入資料庫密碼並確認它會要求使用者。  
  
            伺服器定義識別碼和其對應的加密的密碼會儲存在本機電腦上的檔案  
            
            範例 1：
            
                Specify password
                
                C:\SSMA\SSMAforMySQLConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for MySQL\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for MySQL\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            範例 2：
            
                C:\SSMA\SSMAforMySQLConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for MySQL\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for MySQL\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx
            
    -   **移除加密的密碼**  
  
        執行`SSMAforMySQLConsole.exe`具有`-securepassword`和`-remove`參數在命令列傳遞的伺服器識別碼，若要移除本機電腦上存在的受保護的儲存體檔案加密的密碼。  
  
        範例  

            C:\SSMA\SSMAforMySQLConsole.EXE -securepassword -remove all
            C:\SSMA\SSMAforMySQLConsole.EXE -securepassword -remove "source_1,target_1"  
  
    -   **列出其密碼加密的伺服器識別碼**  
  
        執行`SSMAforMySQLConsole.exe`具有`-securepassword`和`-list`參數在命令列，以列出所有已加密密碼的伺服器識別碼。  
  
        範例  
        
            C:\SSMA\SSMAforMySQLConsole.EXE -securepassword -list  
  
    > [!NOTE]  
    > 1.  指令碼或伺服器連線檔案中所述的純文字密碼的優先於受保護的檔案中的加密密碼。  
    > 2.  當沒有密碼存在於伺服器連線檔案或指令碼檔案的 [伺服器] 區段中，或它有未受保護本機電腦上，主控台會提示您輸入的密碼。  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>匯出或匯入加密的密碼  
SSMA 主控台應用程式可讓您將加密的資料庫密碼存在於本機電腦上的檔案匯出至受保護的檔案，反之亦然。 這有助於讓加密的密碼機器無關。 匯出功能會讀取伺服器識別碼和密碼從本機保護的儲存體，並將資訊儲存在加密的檔案。 系統會提示使用者輸入受保護檔案的密碼。 請確定輸入的密碼是 8 個字元長度，或多個項目。 此受保護的檔案在不同電腦是可攜式的。 匯入功能讀取受保護的檔案從伺服器 id 和密碼資訊。 使用者會提示輸入密碼的受保護的檔案，並將資訊附加到本機受保護的儲存體。  
  
範例  

    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforMySQLConsole.EXE -securepassword -export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforMySQLConsole.EXE -p -e "MySQLDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
範例  

    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforMySQLConsole.EXE -securepassword -import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforMySQLConsole.EXE -p -i "MySQLDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台 (MySQL)](https://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
