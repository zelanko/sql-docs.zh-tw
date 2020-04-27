---
title: bcp_columns |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_columns
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcfbbdb1881662401e791ea197115120444cf855
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63225534"
---
# <a name="bcp_columns"></a>bcp_columns
  設定在使用者檔案中可搭配大量複製在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中進出作業的資料行總數。 [bcp_setbulkmode](bcp-setbulkmode.md)可以用來取代 bcp_columns 和[bcp_colfmt](bcp-colfmt.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_columns (  
HDBC   
hdbc  
,  
INT   
nColumns  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *nColumns*  
 這是使用者檔案中的資料行總數。 即使您準備要將資料從使用者檔案大量複製到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表，而不想複製使用者檔案中的所有資料行，還是必須將*nColumns*設定為使用者檔案資料行的總數。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 只有在使用有效的檔案名呼叫[bcp_init](bcp-init.md)之後，才能呼叫此函式。  
  
 只有打算使用與預設值不同的使用者檔案格式時，才可以呼叫此函數。 如需預設使用者檔案格式之描述的詳細資訊，請參閱**bcp_init**。  
  
 呼叫`bcp_columns`之後，您必須針對使用者檔案中的每個資料行呼叫[bcp_colfmt](bcp-colfmt.md)，以完整定義自訂檔案格式。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
