---
title: 已修正的 bug 清單 |Microsoft Docs
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
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 096c11c018294cbc92b2be13801d6cd953548fff
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264015"
---
# <a name="list-of-bugs-fixed"></a>已修正的 bug 清單

此頁面包含每個版本中已修正的錯誤清單, 從[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 開始[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd"></a>ODBC Driver 17.3 for [!INCLUDE[msCoName](../../includes/msconame_md.md)]的錯誤修正[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 已修正 TCP 傳送通知事件處理記憶體流失
- 已修正 msodbcsql.h 標頭檔中 enum _SQL_FILESTREAM_DESIRED_ACCESS 的重新定義問題
- 已修正 Linux 的 msodbcsql.h 標頭檔中遺失的 ACCESS_TOKEN 和驗證相關定義

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>ODBC Driver 17.2 for [!INCLUDE[msCoName](../../includes/msconame_md.md)]的錯誤修正[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 已修正關於 Azure Active Directory 驗證的錯誤訊息
- 已修正地區設定環境變數以不同方式設定時的編碼偵測
- 已修正連線復原進行中斷連線時的損毀
- 已修正連接活動的偵測
- 已修正關閉通訊端的不正確偵測
- 修正嘗試在失敗復原期間釋放語句控制碼時的無限等候
- 修正在 Windows 上安裝13和17版時不正確的卸載行為
- 已修正舊版 Windows 平臺 (Windows 7、8和 Server 2012) 的解密行為
- 已修正在 Windows 上使用 ADAL 驗證時的快取問題
- 已修正在 Windows 上鎖定和覆寫追蹤記錄的問題

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>ODBC Driver 17.1 for [!INCLUDE[msCoName](../../includes/msconame_md.md)]的錯誤修正[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 修正在呼叫 SQLFreeHandle 時, 如果已啟用 MARS 且連接屬性為 "Encrypt = yes" 時的1秒延遲
- 修正當傳入的緩衝區大小小於所抓取的資料時, SQLGetData 中的錯誤22003損毀 (Windows)
- 已修正截斷的 ADAL 錯誤訊息
- 已修正將浮點數轉換成整數時, 32 位 Windows 上罕見的錯誤
- 已修正將 double 插入具有 Always Encrypted 的十進位欄位時, 會傳回資料截斷錯誤的問題
- 已修正 MacOS 安裝程式的警告
- 已修正當同時啟用連線復原和連線共用時, 將不正確的狀態傳送至 SQL Server, 導致伺服器卸載會話

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>ODBC Driver 17 for [!INCLUDE[msCoName](../../includes/msconame_md.md)]的錯誤修正[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 已修正使用 Kerberos 驗證時的錯誤, 大量插入可能會失敗並出現「拒絕存取」錯誤
- 已移除在2.3.1 以下版本中 unixODBC 錯誤的因應措施 (驅動程式會加倍傳遞至 unixODBC 的特定緩衝區大小)
- 已修正使用 ColumnEncryption = enabled 時的連線恢復功能 (重新連線) 下垂
- 已修正 DSN 建立 bug, 其中使用「Active Directory 互動式驗證」選項時, Azure 驗證視窗可能會變得沒有回應 (Windows)
- 修正在啟用非同步執行 (清除連接控制碼時) 時, ODBC 關閉期間發生的罕見損毀
- 已修正 SQL 驅動程式在執行長時間的預存程式時造成高 CPU 耗用量的問題
- 已修正無法在不轉換的情況下, 于加密的 Varbinary (max) 資料行中抓取資料
- 修正了在靜態資料指標上使用 SQLGetData () 提取 null Varchar (max) 加密資料行之後的問題, 也會為下列資料行, 即使它有資料也一樣
- 已修正使用 Always Encrypted 來提取 Varbinary (max) 欄位的問題
- 已修正 setlocale () 無法使用 Always Encrypted 的問題
- 已修正在 Always Encrypted on 的 XML 類型預存程式參數上呼叫 SQLDescribeParam () 時傳回錯誤的問題
- 已修正無法在 SQLTables 中運作的轉義底線
- 修正在 Linux 上以寬字元傳回時, 希伯來文資料 (Varchar) 被截斷的錯誤 (bug)
- 已修正從 UTF-8 應用程式查詢 Shift-JIS 編碼的 char/Varchar 的問題
- 已修正在 MacOS 上以 SQL_DRIVER_NAME 參數呼叫 SQLGetInfo 的錯誤 (bug) 傳回 Linux 樣式的檔案名
- 已修正載入 Windows-1252 字元資料時, 使用 BCP 公用程式將大於32k 位元組的輸入檔案轉換成 VARCHAR 資料行的問題會導致失敗
