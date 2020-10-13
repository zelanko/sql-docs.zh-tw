---
description: '管理密碼 (AccessToSQL) '
title: 管理密碼 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/01/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b099d0f9-dd37-4c87-8b6f-ed0177881ea4
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3069d1cff693ead8a6acf3af7f9644c4a3d6ab43
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988664"
---
# <a name="managing-passwords-accesstosql"></a>管理密碼 (AccessToSQL) 
本節說明如何保護資料庫密碼以及在伺服器之間匯入或匯出的程式：  
  
1.  保護密碼  
  
2.  匯出或匯入加密的密碼  
  
## <a name="securing-password"></a>保護密碼  
SSMA 可讓您保護資料庫的密碼。  
  
使用下列程式來執行安全連線：  
  
使用下列三種方法之一來指定有效的密碼：  
  
1.  **純文字：** 在 [密碼] 節點的 [值] 屬性中，輸入資料庫密碼。 您可以在腳本檔案或伺服器連接檔案的 [伺服器] 區段的 [伺服器定義] 節點下找到它。  
  
    純文字中的密碼並非安全的。 因此，您將會在主控台輸出中遇到下列警告訊息：「*伺服器 &lt; 伺服器識別碼 &gt; 密碼是以非安全純文字格式提供，SSMA 主控台應用程式提供選項來透過加密保護密碼，請參閱 SSMA 說明檔中的-securepassword 選項以取得詳細資訊。* 」  
  
    **加密的密碼：** 在此案例中，指定的密碼會以加密格式儲存在 ProtectedStorage. ssma 中的本機電腦上。  
  
    -   **保護密碼**  
  
        -   在 `SSMAforAccessConsole.exe` `-securepassword` 命令列中執行，並在命令列上傳遞包含 [伺服器定義] 區段中之 [密碼] 節點的伺服器連接或腳本檔。  
  
        -   提示時，系統會要求使用者輸入資料庫密碼並加以確認。  
  
            伺服器定義識別碼及其對應的加密密碼會儲存在本機電腦上的檔案中。  

            &nbsp;

            _範例 1：_
            
            指定密碼

            ```console
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml"
            ```

            輸入 server_id ' XXX_1 ' 的密碼： >xxxxxxx
                
            重新輸入 server_id ' XXX_1 ' 的密碼： >xxxxxxx  

            &nbsp;

            _範例 2：_

            ```console
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml" -o
            ```

            輸入 server_id ' source_1 ' 的密碼： >xxxxxxx
                
            重新輸入 server_id ' source_1 ' 的密碼： >xxxxxxx
                
            輸入 server_id ' target_1 ' 的密碼： >xxxxxxx
                
            重新輸入 server_id ' target _1 ' 的密碼： >xxxxxxx  
  
    -   **移除加密的密碼**  
  
        `SSMAforAccessConsole.exe` `-securepassword` 在命令列上執行，並 `-remove` 在命令列傳遞伺服器識別碼，以從本機電腦上的受保護儲存體檔案移除加密的密碼。  

        ```console
        C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove all
        C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove "source_1,target_1"
        ```
  
    -   **列出密碼已加密的伺服器識別碼**  
  
        使用來執行 SSMAforAccessConsole.exe， `-securepassword` 並 `-list` 在命令列切換，以列出密碼已加密的所有伺服器識別碼。  

        ```console
        C:\SSMA\SSMAforAccessConsole.EXE -securepassword -list
        ```
  
    > [!NOTE]  
    > 1.  腳本或伺服器連接檔中所述純文字的密碼優先于安全檔案中的加密密碼。  
    > 2.  當伺服器連接檔案或腳本檔案的 [伺服器] 區段中沒有任何密碼，或在本機電腦上未保護密碼時，主控台會提示您輸入密碼。  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>匯出或匯入加密的密碼  
SSMA 主控台應用程式可讓您將本機電腦上的檔案中已加密的資料庫密碼，匯出至安全的檔案，反之亦然。 它有助於讓加密的密碼電腦獨立。 匯出功能會從本機受保護的儲存體讀取伺服器識別碼和密碼，並將資訊儲存在加密的檔案中。 系統會提示使用者輸入受保護檔案的密碼。 請確定輸入的密碼是8個字元以上的長度。 此安全檔案可在不同電腦之間移植。 匯入功能會從受保護的檔案讀取伺服器識別碼和密碼資訊。 系統會提示使用者輸入受保護檔案的密碼，並將資訊附加至本機受保護的存放裝置。  

### <a name="export-password"></a>匯出密碼

1. 輸入密碼以保護匯出的檔案

2. `C:\SSMA\SSMAforAccessConsole.EXE -securepassword -export all "machine1passwords.file"`

3. 輸入密碼以保護匯出的檔案： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

4. 請確認密碼： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

5. `C:\SSMA\SSMAforAccessConsole.EXE -p -e "AccessDB_1_1,Sql_1" "machine2passwords.file"`

6. 輸入密碼以保護匯出的檔案： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

7. 請確認密碼： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  

### <a name="import-an-encrypted-password"></a>匯入加密的密碼

1. 輸入密碼以保護匯入的檔案

2. `C:\SSMA\SSMAforAccessConsole.EXE -securepassword -import all "machine1passwords.file"`

3. 輸入密碼以從加密的檔案匯入伺服器： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

4. 請確認密碼： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

5. `C:\SSMA\SSMAforAccessConsole.EXE -p -i "AccessDB_1,Sql_1" "machine2passwords.file"`

6. 輸入密碼以從加密的檔案匯入伺服器： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

7. 請確認密碼： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  

## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台 (存取) ](./executing-the-ssma-console-accesstosql.md)  
