---
title: 已修正的錯誤 (Bug) 清單
description: 此頁面包含每個版本中已修正的錯誤 (Bug) 清單 (從 Microsoft ODBC Driver 17 for SQL Server 開始)。
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-chojas
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 0541f875230426f6ebc0fd1f90ac06110861f025
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81629718"
---
# <a name="list-of-bugs-fixed"></a>已修正的錯誤 (Bug) 清單

此頁面包含每個版本中已修正的錯誤 (Bug) 清單 (從 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開始)。

### <a name="bug-fixes-in-the-msconame-odbc-driver-1752-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的錯誤 (Bug) 修正

- 已將 msodbcsql.h 新增到 Alpine Linux 套件

### <a name="bug-fixes-in-the-msconame-odbc-driver-175-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的錯誤 (Bug) 修正

- 修正 Linux/macOS 上的 AKV CMK 中繼資料雜湊計算
- 修正載入 OpenSSL 1.0.0 時發生的錯誤
- 修正使用 ISO-8859-1 和 ISO-8859-2 字碼頁時的轉換問題
- 修正 macOS 上的內部程式庫名稱以包含版本號碼
- 修正使用個別長度和指標繫結時，Null 指標的設定

### <a name="bug-fixes-in-the-msconame-odbc-driver-1742-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的錯誤 (Bug) 修正

 - 修正無法正確地將處理序識別碼和應用程式名稱傳送至 SQL Server (用於 sys.databases dm_exec_sessions 分析) 的問題 (Linux)
 - 已移除 libuuid 的多餘相依性 (Linux)
 - 修正將 UTF8 資料傳送至 SQL Server 2019 的錯誤 (Bug)
 - 修正未正確偵測到結尾為 "@euro" 之地區設定的錯誤 (Bug) (Linux)
 - 修正在使用 Always Encrypted 時，擷取為輸出參數時錯誤傳回的 XML 資料

### <a name="bug-fixes-in-the-msconame-odbc-driver-174-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的錯誤 (Bug) 修正

- 修正啟用 Multiple Active Results Sets (MARS) 時的間歇性停止回應
- 修正啟用非同步通知時的連線恢復功能停止回應
- 修正針對多執行緒連接嘗試取得診斷記錄時的損毀
- 修正使用 SQL_USER_NAME 和 SQL_DATA_SOURCE_READ_ONLY 呼叫 SQLGetInfo() 之後重新連線時的「不支援加密」
- 修正 Azure Active Directory 互動式驗證期間的 COM 初始化錯誤
- 修正多位元組 UTF8 資料的 SQLGetData()
- 修正使用 SQLGetData() 擷取 SQL_variant 資料行的長度
- 修正使用 bcp 匯入包含超過 7992 個位元組的 sql_variant 資料行
- 修正針對窄字元資料，將正確編碼傳送至伺服器的問題

### <a name="bug-fixes-in-the-msconame-odbc-driver-173-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的錯誤 (Bug) 修正

- 已修正 TCP 傳送通知事件處理記憶體流失
- 已修正 msodbcsql.h 標頭檔中 enum _SQL_FILESTREAM_DESIRED_ACCESS 的重新定義問題
- 已修正 Linux 的 msodbcsql.h 標頭檔中遺漏的 ACCESS_TOKEN 和 AUTHENTICATION 相關定義

### <a name="bug-fixes-in-the-msconame-odbc-driver-172-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的錯誤 (Bug) 修正

- 已修正 Azure Active Directory 驗證的一個錯誤訊息
- 已修正地區設定環境變數以不同方式設定時的編碼偵測
- 已修正連線復原進行中連線中斷時的損毀
- 已修正偵測連接活躍度的問題
- 已修正不正確偵測已關閉通訊端的問題
- 已修正嘗試在失敗復原期間釋出陳述式控制代碼時的無限等候
- 已修正在 Windows 上安裝 13 和 17 版時不正確的解除安裝行為
- 已修正舊版 Windows 平台 (Windows 7、8 和 Server 2012) 的解密行為
- 已修正在 Windows 上使用 ADAL 驗證時的快取問題
- 已修正在 Windows 上鎖定和覆寫追蹤記錄的問題

### <a name="bug-fixes-in-the-msconame-odbc-driver-171-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的錯誤 (Bug) 修正

- 已修正在已啟用 MARS 且連接屬性為 "Encrypt = yes" 的情況下呼叫 SQLFreeHandle 時的 1 秒延遲
- 已修正當傳入的緩衝區大小小於所擷取的資料時，SQLGetData 中的錯誤 22003 損毀 (Windows)
- 已修正截斷的 ADAL 錯誤訊息
- 已修正將浮點數轉換成整數時，32 位元 Windows 上罕見的錯誤 (Bug)
- 已修正將雙精確度插入具有 Always Encrypted 的十進位欄位時，傳回資料截斷錯誤的問題
- 已修正 macOSS 安裝程式上的警告
- 已修正在工作階段復原嘗試期間，同時啟用 [連線復原] 和 [連線共用] 時，將不正確的狀態傳送至 SQL Server，進而導致伺服器卸除工作階段的問題

### <a name="bug-fixes-in-the-msconame-odbc-driver-17-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的錯誤 (Bug) 修正

- 已修正使用 Kerberos 驗證時，大量插入可能會失敗並出現「存取遭拒」錯誤的錯誤 (Bug)
- 已移除 2.3.1 以下版本中存在之 unixODBC 錯誤 (Bug) 的因應措施 (驅動程式會將傳遞至 unixODBC 的特定緩衝區大小加倍)
- 已修正使用 ColumnEncryption=enabled 時的連線恢復功能 (重新連線) 停止回應
- 已修正 DSN 建立錯誤 (Bug)，其中使用「Active Directory 互動式驗證」選項時，[Azure 驗證] 視窗可能會變成沒有回應 (Windows)
- 已修正在 ODBC 關閉期間啟用非同步執行 (清除連接控制代碼時發生) 時的罕見損毀
- 已修正 SQL 驅動程式在執行長時間的預存程序時造成高 CPU 耗用量的問題
- 已修正無法在不轉換的情況下，擷取加密 varbinary(max) 資料行中資料的問題
- 已修正在靜態資料指標上使用 SQLGetData() 擷取 null varchar(max) 加密資料行之後，即使下列資料行中有資料，也會變成 Null 的問題
- 已修正在開啟 Always Encrypted 時擷取 varbinary(max) 欄位的問題
- 已修正 setlocale() 無法使用 Always Encrypted 的問題
- 已修正在開啟 Always Encrypted 的情況下，對 XML 類型的預存程序參數呼叫 SQLDescribeParam() 時傳回錯誤的問題
- 已修正無法在 SQLTables 中使用逸出底線的問題
- 已修正在 Linux 上以寬字元傳回時，希伯來文資料 (varchar) 遭到截斷的錯誤 (Bug)
- 已修正從 UTF-8 應用程式查詢 Shift-JIS 編碼的 char/varchar 的問題
- 已修正使用 SQL_DRIVER_NAME 參數呼叫 SQLGetInfo 時，在 MacOS 上傳回 Linux 樣式檔案名稱的錯誤 (Bug)
- 已修正載入 Windows-1252 字元資料時，使用 BCP 公用程式將大於 32k 位元組的輸入檔案轉換成 VARCHAR 資料行導致失敗的問題
