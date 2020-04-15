---
title: 可滾動游標和事務隔離 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e40278bd209132736aee2788b5648ffa84a44e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304219"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>可捲動的資料指標和交易隔離
下表列出了管理更改可見性的因素。  
  
|變更:|可見性取決於:|  
|----------------------|----------------------------|  
|資料指標|游標類型,游標實現|  
|同一事務中的其他語句|資料指標類型|  
|其他事務中的報表|游標類型、事務隔離等級|  
  
 這些因素如下圖所示。  
  
 ![管理變更的可見性之因數](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 下表總結了每種游標類型檢測自身、自身事務中的其他操作和其他事務所做的更改的能力。 後一個更改的可見性取決於游標類型和包含游標的事務的隔離級別。  
  
|游標型態\操作|Self|自己<br /><br /> Txn|Othr<br /><br /> Txn<br /><br /> (RU_a])|Othr<br /><br /> Txn<br /><br /> (RC[a])|Othr<br /><br /> Txn<br /><br /> (RR[a])|Othr<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|靜態|||||||  
|插入|也許[b]|否|否|否|否|否|  
|更新|也許[b]|否|否|否|否|否|  
|刪除|也許[b]|否|否|否|否|否|  
|索引鍵集導向的資料指標|||||||  
|插入|也許[b]|否|否|否|否|否|  
|更新|是|是|是|是|否|否|  
|刪除|也許[b]|是|是|是|否|否|  
|動態|||||||  
|插入|是|是|是|是|是|否|  
|更新|是|是|是|是|否|否|  
|刪除|是|是|是|是|否|否|  
  
 [a] 括弧中的字母指示包含游標的事務的隔離級別;另一個事務的隔離級別(進行更改時)不相關。  
  
 RU:讀取未提交  
  
 RC:讀取已提交  
  
 RR:可重複讀取  
  
 S: 序列化  
  
 [b] 取決於游標的實現方式。 游標能否檢測到此類更改是通過**SQLGetInfo**中的SQL_STATIC_SENSITIVITY選項報告的。
