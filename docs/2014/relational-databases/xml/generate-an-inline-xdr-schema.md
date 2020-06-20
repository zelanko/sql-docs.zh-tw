---
title: 產生內嵌 XDR 結構描述 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XDR schemas [SQL Server]
- inline XDR schema generation [SQL Server]
- XMLDATA option
- FOR XML clause, inline XDR schema generation
ms.assetid: 2a40d617-9724-4f7d-80a4-a85c702f14d0
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e2bb7b4b482b79ab5550540dd5b24ffdd8d6636
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061249"
---
# <a name="generate-an-inline-xdr-schema"></a>產生內嵌 XDR 結構描述
  FOR XML 中的 **XMLDATA** 指示詞會將內嵌 XDR 結構描述連同查詢結果一起傳回。 不過，XDR 結構描述並不支援 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本中引進的所有新資料類型和其他的增強功能。 您可以改用 [XMLSCHEMA 指示詞](generate-an-inline-xsd-schema.md)來要求內嵌 XSD 結構描述。  
  
> [!IMPORTANT]  
>  FOR XML 選項的 XMLDATA 指示詞已被取代。 在 RAW 和 AUTO 模式的情況下，請使用 XSD 產生。 EXPLICIT 模式中沒有 XMLDATA 指示詞的替代項目。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 也請注意下列有關於內嵌 XDR 結構描述支援的項目：  
  
-   如果 FOR XML 查詢結果包含 **xml** 類型的資料行，而且您要求內嵌 XDR 結構描述，則會傳回錯誤。 內嵌 XDR 並不支援這些類型。  
  
-   **(n)varchar(max)** 和 **(n)varbinary(max)** 類型會分別對應到 **(n)varchar(n)** 和 **varbinary(n)** 。  
  
-   當相容性模式設定為 90 或更高時， **timestamp** 值會被視為 **varbinary(8)** 資料並當作二進位資料來處理，且會在結果中傳回，如下所示：  
  
    -   如果指定了 **binary base64** ，則會使用 Base 64 編碼。  
  
    -   如果未指定 **binary base64** ，則在 AUTO 模式中會使用 URL 編碼。  
  
  
