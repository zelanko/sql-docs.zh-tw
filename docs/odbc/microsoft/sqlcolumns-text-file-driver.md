---
title: SQLColumns （文字檔案驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColumns
- SQLColumns function [ODBC], Text File Driver
ms.assetid: c99e5f8d-4e43-48f8-9e0e-086707b411f5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34e9f27d1c5c939553d52546f9adbdd92f9d84ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32902523"
---
# <a name="sqlcolumns-text-file-driver"></a>SQLColumns （文字檔案驅動程式）
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|資料行|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|會傳回目錄的路徑。|  
|TABLE_OWNER|因為擁有者名稱不支援此資料行就會傳回 NULL。|  
|NULLABLE|SQL_NO_NULLS 參與的資料行就會傳回主索引鍵或唯一索引。|
