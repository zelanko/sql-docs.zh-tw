---
title: 使用者定義資料類型 (UDT) 的 FOR XML 支援 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 275c6a13b0351bfa95e3d9ac642b1300f88e5c22
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086178"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>使用者自訂資料類型 (UDT) 的 FOR XML 支援
  FOR XML 不支援 Common Language Runtime (CLR) 使用者定義資料類型 (UDT)。  
  
 若要搭配 CLR 使用者定義資料類型使用 FOR XML，請確定此資料類型有 XML 序列化，並在 FOR XML SELECT 子句中使用 XML 的明確轉換。  
  
## <a name="see-also"></a>另請參閱  
 [各個 SQL Server 資料類型的 FOR XML 支援](for-xml-support-for-various-sql-server-data-types.md)  
  
  
