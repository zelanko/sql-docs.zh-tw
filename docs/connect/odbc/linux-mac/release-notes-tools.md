---
title: Linux 與 macOS 上 mssql-tools 的版本資訊
description: 了解 Microsoft SQL Server 工具發行版本的新功能與變更。
ms.custom: ''
ms.date: 07/13/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-zhangw
ms.author: v-zhangw
manager: kenvh
ms.openlocfilehash: 85f7115dbf138055df83a7bb07e5a78f505b5794
ms.sourcegitcommit: 6f49804b863fed44968ea5829e2c26edc5988468
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/05/2020
ms.locfileid: "87812351"
---
# <a name="release-notes-for-the-microsoft-sql-server-tools-on-linux-and-macos"></a>Linux 與 macOS 上的 Microsoft SQL Server 工具版本資訊

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

此文章列出並描述 Linux 與 macOS 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] SQL Server 工具發行版本的新功能。

## <a name="17611-july-2020"></a>17.6.1.1，2020 年 7 月

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 已更新 Sqlcmd 命令列剖析器 | 已修正以不同的順序使用特定選項時會發生非預期行為的錯誤 (Bug)。 |
| 已更新 Sqlcmd 錯誤訊息 | 已修正 sqlcmd 中錯誤傳回方式的各種不一致。 |
| 已修正 Sqlcmd -Y 選項 | 已修正 -Y 選項無效的問題 |
| 已修正 Sqlcmd 資料行名稱截斷 | 已修正資料行名稱會不正確地截斷的問題 |
| Sqlcmd Linux 結束代碼 | 已修正 Linux 上遺漏處理序結束代碼的問題 |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>後續步驟

深入了解如何使用 [BCP](connecting-with-bcp.md) 與 [SQLCMD](connecting-with-sqlcmd.md) 進行連線！
