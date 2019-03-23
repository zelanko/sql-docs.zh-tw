---
title: Integration Services 角色 (SSIS 服務) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], roles
- db_ssisoperator role
- db_ssisadmin role
- fixed database roles [Integration Services]
- packages [Integration Services], security
- roles [Integration Services]
- db_ssisltduser role
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 43c1c932565ae3df666be10a1b89794ecd720135
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393026"
---
# <a name="integration-services-roles-ssis-service"></a>Integration Services 角色 (SSIS 服務)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含三個固定的資料庫層級角色中， `db_ssisadmin`， **db_ssisltduser**，以及**db_ssisoperator**，用於控制封裝的存取權。 只能在儲存至封裝上實作角色`msdb`資料庫中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]將角色指派給封裝。 角色指派會儲存到`msdb`資料庫。  
  
## <a name="read-and-write-actions"></a>讀取和寫入動作  
 下表描述 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中 Windows 及固定資料庫層級角色的讀取和寫入動作。  
  
|角色|讀取動作|寫入動作|  
|----------|-----------------|------------------|  
|`db_ssisadmin`<br /><br /> 中的多個<br /><br /> `sysadmin`|列舉自己的封裝。<br /><br /> 列舉所有封裝。<br /><br /> 檢視自己的封裝。<br /><br /> 檢視所有封裝。<br /><br /> 執行自己的封裝。<br /><br /> 執行所有封裝。<br /><br /> 匯出自己的封裝。<br /><br /> 匯出所有封裝。<br /><br /> 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 中的所有封裝。|匯入封裝。<br /><br /> 刪除自己的封裝。<br /><br /> 刪除所有封裝。<br /><br /> 變更自己的封裝角色。<br /><br /> 變更所有封裝角色。<br /><br /> <br /><br /> **\*\* 重要\* \***  db_ssisadmin 角色和 dc_admin 角色的成員可以將其權限提高為系統管理員。 之所以能夠進行此權限提高，是因為這些角色可以修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，而且 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可藉由使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 sysadmin 安全性內容由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行。 若要在執行維護計畫、資料收集組和其他 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時預防此權限提高，請將執行封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業設為使用有限權限的 Proxy 帳戶，或是只將系統管理員 (sysadmin) 成員加入 db_ssisadmin 和 dc_admin 角色。|  
|**db_ssisltduser**|列舉自己的封裝。<br /><br /> 列舉所有封裝。<br /><br /> 檢視自己的封裝。<br /><br /> 執行自己的封裝。<br /><br /> 匯出自己的封裝。|匯入封裝。<br /><br /> 刪除自己的封裝。<br /><br /> 變更自己的封裝角色。|  
|**db_ssisoperator**|列舉所有封裝。<br /><br /> 檢視所有封裝。<br /><br /> 執行所有封裝。<br /><br /> 匯出所有封裝。<br /><br /> 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 中的所有封裝。|None|  
|**Windows administrators**|檢視所有正在執行之封裝的執行詳細資料。|停止所有目前正在執行的封裝。|  
  
## <a name="sysssispackages-table"></a>Sysssispackages 資料表  
 **Sysssispackages**資料表中`msdb`包含的封裝儲存到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 [sysssispackages &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql)。  
  
 **sysssispackages** 資料表包括的資料行包含指派給封裝之角色的相關資訊。  
  
-   **readerrole** 資料行會指定擁有封裝之讀取權限的角色。  
  
-   **writerrole** 資料行會指定擁有封裝之寫入權限的角色。  
  
-   **ownersid** 資料行包含建立封裝之使用者的唯一安全性識別碼。 此資料行會定義封裝的擁有者。  
  
## <a name="permissions"></a>Permissions  
 根據預設的權限`db_ssisadmin`並**db_ssisoperator**固定的資料庫層級角色和建立封裝之使用者的唯一安全性識別碼適用於套件和權限的讀取者角色`db_ssisadmin`角色和建立封裝之使用者的唯一安全性識別碼適用於寫入者角色。 使用者必須是隸屬`db_ssisadmin`， **db_ssisltduser**，或**db_ssisoperator**角色，才能擁有封裝的讀取權限。 使用者必須是成員`db_ssisadmin`角色具有寫入存取權。  
  
## <a name="access-to-packages"></a>對封裝的存取權  
 固定資料庫層級角色要與使用者定義角色搭配使用。 使用者定義角色是您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中建立後用以指派權限給封裝的角色。 若要存取封裝，使用者必須是使用者定義角色和適當 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 固定資料庫層級角色的成員。 例如，如果使用者屬於**AuditUsers**指派給封裝的使用者定義角色，他們還必須是成員`db_ssisadmin`， **db_ssisltduser**，或**db_ssisoperator**角色，才能擁有封裝的讀取權限。  
  
 如果您沒有指派使用者定義角色給封裝，則對封裝的存取是由固定的資料庫層級角色決定的。  
  
 如果您想要使用使用者定義的角色，您必須將他們新增`msdb`資料庫，才能將它們指派給封裝。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中建立新資料庫角色。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料庫層級角色會授與 msdb 資料庫中 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 系統資料表的權限。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須先啟動 （MSSQLSERVER 服務），您可以連接到 Database Engine 並存取`msdb`資料庫。  
  
 若要將角色指派給封裝，您需要完成下列工作。  
  
-   **開啟物件總管並連接到 Integration Services**  
  
     必須先在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中開啟 [物件總管]，並連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，才能使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]指派角色給封裝。  
  
     必須先啟動 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，才能連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
-   **指派讀取器和寫入器角色給封裝**  
  
     您可將讀取器和寫入器角色指派給每個封裝。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [指派讀取器和寫入器角色給套件](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [建立使用者定義角色](../create-a-user-defined-role.md)  
  
-   [連接到 Integration Services](../connect-to-integration-services.md)  
  
  
