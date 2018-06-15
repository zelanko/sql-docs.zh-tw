---
title: 對應來源和目標資料庫 (AccessToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: eb290594fc878a2df4cd6345ce6f9cc8f86ff51d
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773824"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>對應來源和目標資料庫 (AccessToSQL)
當您連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您需要指定移轉的目標資料庫。 如果您有多個存取資料庫可以將其對應至多個[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫 （或結構描述），或在連接的 SQL Azure 資料庫的多個結構描述。  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server 或 SQL Azure 資料庫結構描述  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫會使用結構描述的概念，區隔成邏輯群組的資料庫內的物件。 例如，程式庫資料庫可以使用三個結構描述，名為**書籍**，**音訊**，和**視訊**彼此分隔活頁簿，音訊及視訊的物件。 根據預設，access 資料庫對應至**主要**資料庫和**dbo**結構描述中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和連接的資料庫和**dbo** SQL Azure 中的結構描述。  
  
除非您自訂每個存取資料庫之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫和結構描述，SSMA 會將所有結構描述和對應的預設資料庫的 access 資料庫相關聯的資料移轉。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和結構描述  
SSMA 可讓您對應至每個存取資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫和結構描述。 下列程序描述如何自訂每個資料庫的對應。  
  
**若要修改的目標資料庫和結構描述**  
  
1.  在存取中繼資料總管 窗格中，選取**存取中繼資料**。  
  
    結構描述對應也會提供當您選取**資料庫**節點或任何資料庫節點。 所選物件的自訂結構描述的對應清單。  
  
2.  在右窗格中，按一下 [**結構描述對應**] 索引標籤。  
  
    您會看到資料表，其中包含存取資料庫名稱和其相對應的 n 或 Sql Azure 結構描述。 目標結構描述中的兩個組件標記法 (database.schema) 表示。  
  
3.  選取包含您要自訂，然後按一下的對應的資料列**修改**。  
  
4.  在**選擇目標結構描述**對話方塊中，您可能瀏覽可用的目標資料庫和結構描述或型別資料庫結構描述] 文字方塊中的兩個組件標記法 (database.schema) 中的名稱，然後按一下 [**確定**。  
  
**對應的模式**  
  
-   對應至 SQL Server  
  
您可以將來源資料庫對應到任何目標資料庫。 依預設，來源資料庫都會對應到目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]與您已經連接使用 SSMA 的資料庫。 如果正在對應之目標資料庫不存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，則會以訊息提示您 **」 資料庫及/或結構描述不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料。它會建立同步處理期間。您要繼續嗎？ 」** 按一下 [是]。 同樣地，您可以將對應結構描述不存在目標結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]同步處理期間所建立的資料庫。  
  
-   對應至 SQL Azure  
  
您可以將來源資料庫對應至連接的目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫或連接的目標中的任何結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。 如果您將來源結構描述對應至連接的目標資料庫底下的任何非現有結構描述，則系統將提示您使用訊息 **」 結構描述不存在於目標中繼資料。它會建立同步處理期間。您要繼續嗎？"** 按一下 [是]。  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>還原到您的初始資料庫和結構描述  
如果您自訂的 Access 資料庫之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫和結構描述，您可以還原回您指定當您連接到資料庫對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
**若要重設為預設資料庫和結構描述**  
  
1.  結構描述對應索引標籤下選取任何資料列，然後按一下**重設為預設**還原為預設的資料庫和結構描述。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[轉換資料庫物件](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
