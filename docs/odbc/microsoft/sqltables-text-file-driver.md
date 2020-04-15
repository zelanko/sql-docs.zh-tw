---
title: SQLTables(文字檔案驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 938ceba5da25d176628d5c1d9875383d977e3aec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299328"
---
# <a name="sqltables-text-file-driver"></a>SQLTables (文字檔驅動程式)
> [!NOTE]  
>  本主題提供特定於文本檔驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|引數|註解|  
|--------------|--------------|  
|*szTable 擁有者*|*szTableOwner*的唯一有效參數是 NULL,因為沒有任何驅動程式支援擁有者名稱。 將*szTableOwner*設定為 NULL 時,將傳回所有表。 NULL 在TABLE_OWNER列中返回。|  
|*szTable限定*|在TABLE_QUALIFIER列中 **,SQLTables**將路徑傳回到目錄。|  
|*SzTable 類型*|"TABLE"是唯一支援的表類型。<br /><br /> 使用文字驅動程式時 **,SQLTables**傳回的檔案清單由**ODBC 文本設定**對話方塊中的 **「擴展清單」** 框中的檔案延伸名確定。|
