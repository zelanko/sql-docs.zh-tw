---
title: 自動提交模式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f19053eec7a48eba7a51425b01744f3acd10015
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285108"
---
# <a name="auto-commit-mode"></a>自動認可模式
*在自動提交模式下,* 每個資料庫操作都是執行時提交的事務。 此模式適用於由單個 SQL 語句組成的許多實際事務。 沒有必要對這些事務的完成進行分隔或指定。 在沒有事務支援的資料庫中,自動提交模式是唯一支援的模式。 在此類資料庫中,語句在執行時被提交,無法回滾它們;因此,它們始終處於自動提交模式。  
  
 如果基礎 DBMS 不支援自動提交模式事務,則驅動程式可以通過在執行每個 SQL 語句時手動提交來模擬它們。  
  
 如果在自動提交模式下執行一批 SQL 語句,則當提交批處理中的語句時,它是特定於數據源的。 它們可以在執行時提交,也可以在整個批處理執行后作為一個整體提交。 某些數據源可能支援這兩種行為,並可能提供一種選擇其中一種或另一種行為的方法。 特別是,如果批處理中間發生錯誤,則是特定於數據源的語句,無論是已提交還是回滾已執行的語句。 因此,使用批處理並要求它們作為整體提交或回滾的可互操作應用程式應僅在手動提交模式下執行批處理。
