---
title: 已修正的 bug 清單 |Microsoft 文件
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: genemi
manager: kenvh
ms.workload: Active
ms.openlocfilehash: 5187e07d18c6a967ce0a8fadbac370273684c9dc
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2018
---
# <a name="list-of-bugs-fixed"></a>已修正的 bug 的清單

此頁面包含在開頭的每個版本中修正的 bug 清單[!INCLUDE[msCoName](../../includes/msconame_md.md)]的 ODBC 驅動程式 17 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>中的 bug 修正[!INCLUDE[msCoName](../../includes/msconame_md.md)]的 ODBC 驅動程式 17.1 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- 呼叫啟用 mars SQLFreeHandle 和連接屬性時，將修復 1 秒延遲"Encrypt = yes"
- 修正錯誤 22003 損毀時傳入緩衝區的大小較小的 SQLGetData 然後所擷取的資料 (Windows)
- 固定截斷 ADAL 的錯誤訊息
- 32 位元 Windows 上固定極少數的 bug，當轉換浮點數到整數
- 修正的問題，其中會插入 double with Always Encrypted 十進位欄位上沒有傳回資料截斷錯誤
- 固定 MacOS 安裝程式警告
- 修正不正確的狀態時傳送給 SQL Server 工作階段復原嘗試期間連接恢復功能和連線集區都已啟用，導致工作階段卸除的伺服器

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>中的 bug 修正[!INCLUDE[msCoName](../../includes/msconame_md.md)]的 ODBC 驅動程式 17 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- 修正的 bug 其中使用 Kerberos 驗證時，大量插入可能會失敗，發生 「 拒絕存取 」 錯誤
- UnixODBC bug 2.3.1 下方的版本中移除的因應措施 （驅動程式會加倍傳遞至 unixODBC 特定緩衝區的大小）
- 固定連接恢復功能 （重新連線） 溢出時使用 ColumnEncryption = 啟用
- 修正 DSN 建立 bug，其中時使用 [Active Directory 互動式驗證] 選項 Azure Authentication 視窗可能會變得沒有回應 (Windows)
- （發生什麼事時清除連接控制代碼） 來啟用非同步執行時，ODBC 關機期間固定極少數的損毀
- 已修正下列問題其中 SQL 驅動程式造成高 CPU 耗用率時執行長時間的預存程序
- 固定或是無法抓取加密的 varbinary （max） 資料行不需要轉換中的資料
- 其中之後 null 的 varchar （max） 加密的資料行擷取靜態資料指標上使用 SQLGetData() 修正的問題，下列資料行是也 nulled 即使它有資料
- 修正的問題上擷取 varbinary （max） 欄位，使用 永遠加密
- 修正的問題的 setlocale() 不使用永遠加密
- SQLDescribeParam() 傳回上呼叫上使用 永遠加密的 XML 類型的預存程序參數時的錯誤修正的問題
- 修正逸出的底線 SQLTables 中無法運作
- 修正的 bug 其中希伯來文資料 (varchar) 會遭到截斷 Linux 上傳回做為寬字元
- 已修正的問題與查詢 SHIFT-JIS 編碼 char/varchar 從 utf-8 應用程式
- 修正 bug MacOS 上呼叫 SQLGetInfo SQL_DRIVER_NAME 參數與傳回其中 Linux 樣式檔名
- 已修正下列問題其中載入 windows-1252 字元資料，使用輸入檔案大於 32k 成使用 BCP 公用程式的 VARCHAR 資料行的位元組會導致失敗
