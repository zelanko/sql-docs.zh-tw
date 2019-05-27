---
title: 取得完整記憶體傾印以針對 SQL Server Management Studio (SSMS) 進行疑難排解
Description: 透過收集完整記憶體傾印，針對 SSMS 停止回應或當機進行疑難排解
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: how-to
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: dineth, sstein
ms.custom: ''
ms.date: 05/17/2019
ms.openlocfilehash: ff78af4ffcfe530ba28d47ec57852486523f859a
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2019
ms.locfileid: "65822506"
---
# <a name="get-full-memory-dump"></a>取得完整記憶體傾印

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

在本文中，您會學習如何擷取診斷資訊，針對使用 SQL Server Management Studio (SSMS) 時發生的當機或停止回應進行疑難排解。

若要擷取診斷資訊以進行疑難排解，請遵循下列步驟。

1. 下載 [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)。

2. 將下載項目解壓縮到資料夾。

3. 開啟命令提示字元，並執行下列命令。

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    它應該會提示您接受授權合約，請選取 [同意]。

4. 啟動 SQL Server Management Studio (SSMS) (若尚未啟動的話)。

5. 重現您的問題。

6. 命令提示字元中應該會顯示與寫入傾印檔有關的文字，請等待它完成。

7. 建立新資料夾，並將寫出的 *.dmp 檔案複製到該資料夾。

8. 將下列檔案複製到相同的資料夾。

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. 壓縮資料夾。

## <a name="outofmemoryexception"></a>OutOfMemoryException

您也可以在 SSMS 擲回 OutOfMemoryException (可能是任何受控例外狀況) 時，取得 SSMS 的完整記憶體傾印。

若要擷取診斷資訊以針對 SSMS 的 OutOfMemoryException 進行疑難排解，請遵循下列步驟。

1. 下載 [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)。

2. 將下載項目解壓縮到資料夾。

3. 開啟命令提示字元，並執行下列命令。

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    它應該會提示您接受授權合約，請選取 [同意]。

4. 啟動 SQL Server Management Studio (若尚未啟動的話)。

5. 重現問題。

6. 命令提示字元中應該會顯示與寫入傾印檔有關的文字，請等待它完成。

7. 建立新資料夾，並將寫出的 *.dmp 檔案複製到該資料夾。

8. 將下列檔案複製到相同的資料夾。

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. 壓縮資料夾。

## <a name="next-steps"></a>後續步驟

[Transact-SQL](../sql-server-management-studio-ssms.md)