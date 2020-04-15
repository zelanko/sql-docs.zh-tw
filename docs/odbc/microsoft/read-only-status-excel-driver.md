---
title: 唯讀狀態(Excel 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb585d4712b6cac5e09b65ee8e13604763cd0164
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304019"
---
# <a name="read-only-status-excel-driver"></a>唯讀狀態 (Excel 驅動程式)
使用 Microsoft Excel 驅動程式時,預設情況下,數據源表作為唯讀表打開,並且一次只能由一個使用者打開。 但是,即使表具有唯讀狀態,應用程式也可以對 Microsoft Excel 表執行插入和更新。  
  
 當應用程式透過 Microsoft Excel 驅動程式對 Microsoft Excel 資料執行「保存為」命令時,應用程式應創建一個新表並將要儲存的資料插入到新表中。 插入會導致表追加。 在表關閉並重新打開之前,無法對表執行任何其他操作。 關閉表後,無法執行後續插入,因為該表是唯讀表。  
  
 使用 Microsoft Excel 驅動程式時可以更新值,但不能從基於 Microsoft Excel 電子表格的表中刪除行,因此 Microsoft Excel 驅動程式不被視為正式支援更新。
