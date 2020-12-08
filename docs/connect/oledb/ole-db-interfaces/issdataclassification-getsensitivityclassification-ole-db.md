---
title: ISSDataClassification::GetSensitivityClassification | Microsoft Docs
description: ISSDataClassification::GetSensitivityClassification
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSDataClassification::GetSensitivityClassification
apitype: COM
helpviewer_keywords:
- GetSensitivityClassification method
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 04877e626b57022d0110501b7da6145b2c4997d2
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506649"
---
# <a name="issdataclassificationgetsensitivityclassification"></a>ISSDataClassification::GetSensitivityClassification
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../../includes/applies-to-version/sql-asdb-asa.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  針對作用中的資料列集擷取敏感性分類資料。 如需詳細資訊與程式碼範例，請參閱[使用資料分類](../features/using-data-classification.md)。  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT GetSensitivityClassification(
    SENSITIVITYCLASSIFICATION** ppSensitivityClassification);
```  
  
## <a name="arguments"></a>引數  
  *ppSensitivityClassification*[out]  
 指向 SENSITIVITYCLASSIFICATION 結構指標的指標。 如果方法失敗，或者沒有可用的資料分類資訊，提供者就不會配置任何記憶體，也無法確保輸出時，ppSensitivityClassification 引數為 Null 指標。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。    
  
 E_INVALIDARG  
 *ppSensitivityClassification* 引數為 NULL。  
  
 E_OUTOFMEMORY  
 OLE DB Driver for SQL Server 無法配置足夠的記憶體來完成要求。  

  
## <a name="remarks"></a>備註  
OLE DB Driver for SQL Server 會配置記憶體區塊以保存 SENSITIVITYCLASSIFICATION 結構，以及此結構所參考的資料。 當取用者不再需要存取分類資料時，其必須呼叫 [IMalloc::Free](https://docs.microsoft.com/windows/win32/api/objidl/nf-objidl-imalloc-free) \(英文\) 方法來將這個記憶體解除配置。  
  
 SENSITIVITYCLASSIFICATION 結構的定義如下：
  
```cpp
typedef struct tagSensitivityClassification
{
    USHORT                     cSensitivityLabels;
    SENSITIVITYLABEL          *rgSensitivityLabels;
    USHORT                     cInformationTypes;
    INFORMATIONTYPE           *rgInformationTypes;
    USHORT                     cColumnSensitivityMetadata;
    COLUMNSENSITIVITYMETADATA *rgColumnSensitivityMetadata;
    SENSITIVITYRANKENUM        eQuerySensitivityRank;
} SENSITIVITYCLASSIFICATION;
```  

|member|描述|  
|------------|-----------------|  
|*cSensitivityLabels*|*rgSensitivityLabels* 中 SENSITIVITYLABEL 結構的數目。|  
|*rgSensitivityLabels*|SENSITIVITYLABEL 結構的陣列。|  
|*cInformationTypes*|*rgInformationTypes* 中 INFORMATIONTYPE 結構的數目。|  
|*rgInformationTypes*|INFORMATIONTYPE 結構的陣列。|  
|*cColumnSensitivityMetadata*|*rgColumnSensitivityMetadata* 中 COLUMNSENSITIVITYMETADATA 結構的數目。|  
|*rgColumnSensitivityMetadata*|COLUMNSENSITIVITYMETADATA 結構的陣列。|  
|*eQuerySensitivityRank*|執行來取得資料列集之查詢的敏感性相對順位。|  

SENSITIVITYLABEL 結構的定義如下：
```cpp
typedef struct tagSENSITIVITYLABEL
{
    LPOLESTR pwszName;
    LPOLESTR pwszId;
} SENSITIVITYLABEL;
```

|member|描述|  
|------------|-----------------|  
|*pwszName*|敏感度標籤的名稱。|  
|*pwszId*|敏感度標籤的識別碼。|  

INFORMATIONTYPE 結構的定義如下：
```cpp
typedef struct tagINFORMATIONTYPE
{
    LPOLESTR pwszName;
    LPOLESTR pwszId;
} INFORMATIONTYPE;
```

|member|描述|  
|------------|-----------------|  
|*pwszName*|資訊類型的名稱。|  
|*pwszId*|資訊類型的識別碼。|  

COLUMNSENSITIVITYMETADATA 結構的定義如下：
```cpp
typedef struct tagCOLUMNSENSITIVITYMETADATA
{
    SENSITIVITYPROPERTY* rgSensitivityProperties;
    USHORT cSensitivityProperties;
} COLUMNSENSITIVITYMETADATA;
```

|member|描述|  
|------------|-----------------|  
|*cSensitivityProperties*|*rgSensitivityProperties* 中 SENSITIVITYPROPERTY 結構的數目。|  
|*rgSensitivityProperties*|SENSITIVITYPROPERTY 結構的陣列。|  

SENSITIVITYRANKENUM 列舉的定義如下：
```cpp
typedef enum tagSENSITIVITYRANKENUM
{
    SENSITIVITYRANK_NOT_DEFINED = -1,
    SENSITIVITYRANK_NONE = 0,
    SENSITIVITYRANK_LOW = 10,
    SENSITIVITYRANK_MEDIUM = 20,
    SENSITIVITYRANK_HIGH = 30,
    SENSITIVITYRANK_CRITICAL = 40
} SENSITIVITYRANKENUM;
```

SENSITIVITYPROPERTY 結構的定義如下：
```cpp
typedef struct tagSENSITIVITYPROPERTY
{
    SENSITIVITYLABEL* pSensitivityLabel;
    INFORMATIONTYPE* pInformationType;
    SENSITIVITYRANKENUM eSensitivityRank;
} SENSITIVITYPROPERTY;
```

|member|描述|  
|------------|-----------------|  
|*pSensitivityLabel*|指向 SENSITIVITYLABEL 結構的指標。|  
|*pInformationType*|指向 INFORMATIONTYPE 結構的指標。|  
|*eSensitivityRank*|屬於個別資料行資料之資料行的敏感性相對順位。|  

## <a name="see-also"></a>另請參閱  
 [ISSDataClassification](../../oledb/ole-db-interfaces/issdataclassification-ole-db.md)  
 [資料列集](../ole-db-rowsets/rowsets.md)  
  
