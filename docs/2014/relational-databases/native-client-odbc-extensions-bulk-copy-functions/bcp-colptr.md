---
title: bcp_colptr |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_colptr
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 38e4b2590bebd09da764e6249e59d32b0c28d356
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705304"
---
# <a name="bcp_colptr"></a>bcp_colptr
  將目前副本的程式變數資料位址設定成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_colptr (  
HDBC   
hdbc  
,  
LPCBYTE   
pData  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *pData*  
 這是要複製之資料的指標。 如果系結的資料類型是大數數值型別（例如 SQLTEXT 或 SQLIMAGE），則*pData*可以是 Null。 Null *pData*表示 long 資料值將使用[bcp_moretext](bcp-moretext.md)以區區塊轉送至 SQL Server。  
  
 如果*pData*設定為 Null，且對應至系結欄位的資料行不是大數數值型別， **bcp_colptr**會失敗。  
  
 如需有關大數數值型別的詳細資訊，請參閱[bcp_bind](bcp-bind.md)**。**  
  
 *idxServerCol*  
 這是資料庫資料表中要將資料複製到其中之資料行的序數位置。 資料表中的第一個資料行是資料行 1。 資料行的序數位置是由[SQLColumns](../native-client-odbc-api/sqlcolumns.md)所報告。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 當您將資料複製到具有[bcp_sendrow](bcp-sendrow.md)的 SQL Server 時， **bcp_colptr**函數可讓您變更特定資料行的來源資料位址。  
  
 一開始，使用者資料的指標是由**bcp_bind**的呼叫所設定。 如果程式變數資料位址在**bcp_sendrow**的呼叫之間變更，您可以呼叫**bcp_colptr** ，將指標重設為數據。 下一次呼叫**bcp_sendrow**會將呼叫所定址的資料傳送給**bcp_colptr**。  
  
 您想要修改其資料位址之資料表中的每個資料行都必須有個別的**bcp_colptr**呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
