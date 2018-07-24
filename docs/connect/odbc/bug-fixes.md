---
title: 已修正的 bug 清單 |Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 3b5969a723b230139b9466f75569375f97a0d7b0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2018
ms.locfileid: "37946902"
---
# <a name="list-of-bugs-fixed"></a>已修正的 bug 的清單

此頁面包含在每個版本中，從已修正的 bug 清單[!INCLUDE[msCoName](../../includes/msconame_md.md)]ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversionmdmd"></a>中的錯誤修正[!INCLUDE[msCoName](../../includes/msconame_md.md)]的 ODBC 驅動程式 17.2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- 已修正有關 Azure Active Directory 驗證的錯誤訊息
- 已修正編碼偵測時以不同的方式設定地區設定環境變數
- 固定連線復原進行中時中斷連線時當機
- 已修正的偵測連線作用的
- 已修正不正確的偵測，關閉通訊端
- 嘗試釋放陳述式控制代碼失敗的復原時，已修正無限期等候
- 13 和 17 這兩種版本安裝在 Windows 上時，已修正不正確的解除安裝行為
- 在舊版的 Windows 平台 (Windows 7、windows 8 和 Server 2012) 上的固定的解密行為
- Windows 上使用 ADAL 驗證時，已修正快取問題
- 修正會被鎖定的問題，並在 Windows 上覆寫追蹤記錄

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>中的錯誤修正[!INCLUDE[msCoName](../../includes/msconame_md.md)]的 ODBC 驅動程式 17.1 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- 呼叫啟用 mars 的 SQLFreeHandle 和連接屬性時，已修正 1 秒延遲 「 Encrypt = yes"
- 修正錯誤 22003 損毀，在 SQLGetData 時傳入緩衝區的大小較小，則所擷取的資料 (Windows)
- 已修正截斷的 ADAL 錯誤訊息
- 修正了罕見 32 位元 Windows 上時轉換浮點數到整數
- 已修正的問題，十進位的欄位，透過 Always Encrypted 上插入雙引號將會傳回資料截斷錯誤
- 修正 MacOS 安裝程式警告
- 已修正不正確的狀態時傳送給 SQL Server 工作階段復原嘗試期間連線恢復功能和連接共用這兩個已啟用，導致工作階段卸除的伺服器

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>中的錯誤修正[!INCLUDE[msCoName](../../includes/msconame_md.md)]ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- 修正了在使用 Kerberos 驗證時，大量插入可能會失敗，發生 「 拒絕存取 」 錯誤
- 已移除的因應措施，針對出現在版本低於 2.3.1 unixODBC bug （驅動程式會加倍傳遞至 unixODBC 特定緩衝區的大小）
- 已修正連接恢復功能 （重新連線） 停止回應時使用 ColumnEncryption = 啟用
- 已修正 DSN 建立 bug，其中時使用 「 Active Directory 互動式驗證 」 選項 Azure 驗證視窗可能會變得沒有回應 (Windows)
- （發生在清除連接控制代碼） 來啟用非同步執行時，ODBC 關機期間固定的罕見損毀
- 已修正的問題，SQL 驅動程式會造成執行長時間的預存程序時的高 CPU 耗用量
- 修正的無法在沒有轉換的加密 varbinary （max） 資料行中擷取資料
- 修正的問題之後為 null 的 varchar （max）, 加密的資料行擷取靜態資料指標上使用 SQLGetData()，下列資料行是也 nulled 它在沒有資料
- 已修正的問題上擷取 varbinary （max） 欄位，使用 永遠加密
- 已修正未使用 Always Encrypted 的 setlocale() 的問題
- SQLDescribeParam() 傳回上呼叫上使用 永遠加密的 XML 類型的預存程序參數時的錯誤修正的問題
- 已修正在 SQLTables 中無法運作的逸出的底線
- 已修正的 bug，希伯來文的資料 (varchar) 會被截斷以寬字元傳回在 Linux 上
- 已修正的問題查詢 Shift JIS 編碼 char/varchar 從 utf-8 應用程式
- 已修正的 bug 在 MacOS 上使用 SQL_DRIVER_NAME 參數呼叫 SQLGetInfo 傳回位置 Linux 樣式的檔名
- 已修正的問題，載入 Windows 1252 的字元資料，使用輸入檔案大於 32k，到使用 BCP 公用程式的 VARCHAR 資料行的位元組會導致失敗
