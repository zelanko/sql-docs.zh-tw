---
title: 針對使用 SQL Server Management Studio (SSMS) 時發生的當機或損毀問題進行疑難排解
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: dnethi
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
manager: jroth
ms.custom: ''
ms.date: 07/01/2019
ms.openlocfilehash: 424b0863da9d0d2cfb56676bed5c368efc4d9349
ms.sourcegitcommit: 0b0f5aba602732834c8439c192d95921149ab4c3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2019
ms.locfileid: "67501185"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>在 SQL Server Management Studio (SSMS) 損毀之後取得診斷資料

[!INCLUDE[適用於](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)

## <a name="get-full-memory-dump-of-sql-server-management-studio-ssms-when-it-hangs-or-crashes"></a>取得 SQL Server Management Studio (SSMS) 當機或損毀時的完整記憶體傾印

若要擷取診斷資訊以針對 SSMS 損毀或當機進行疑難排解，請遵循下列步驟。

1. 下載 [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)。

2. 將下載項目解壓縮到資料夾。

3. 開啟命令提示字元，並執行下列命令。

    ```command prompt  <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    If it prompts you to accept a license agreement, select *Agree*.

4. Start SSMS, if it hasn't started already.

5. Reproduce the issue.

6. The text should appear in the cmd prompt about writing the dump file, wait for that to finish.

7. Create a new folder and copy the *.dmp file that is written out to that folder.

8. Copy the following files into the same folder.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Zip up the folder

## Get full memory dump of SSMS when it throws an OutOfMemoryException

You can get a full memory dump with any managed exception.

To capture diagnostic information to troubleshoot an OutOfMemoryException from SSMS, follow the steps below.

1. Download [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Unzip the download into a folder.

3. Open Command Prompt and run the following command.

    ```command prompt
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    若它提示您接受授權合約，請選取 [同意]  。

4. 啟動 SQL Server Management Studio (若尚未啟動的話)。

5. 重現問題。

6. 命令提示字元中應該會顯示與寫入傾印檔有關的文字，請等待它完成。

7. 建立新資料夾，並將寫出的 *.dmp 檔案複製到該資料夾。

8. 將下列檔案複製到相同的資料夾。

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. 壓縮資料夾。