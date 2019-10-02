---
title: Eseguire la migrazione delle risorse
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Eseguire la migrazione delle risorse
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: d14ee6491e4fc804d6545c6708f1d27a44c83501
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224066"
---
# <a name="migrate-assets-infrastructure-apps-and-data"></a>Eseguire la migrazione delle risorse (infrastruttura, app e dati)

In questa fase del percorso si usa l'output della fase di valutazione per avviare la migrazione dell'ambiente. Questa guida consente di identificare gli strumenti appropriati per raggiungere uno "stato completato", inclusi strumenti nativi, strumenti di terze parti e strumenti di gestione del progetto.

# <a name="native-migration-toolstabtools"></a>[Strumenti di migrazione nativi](#tab/Tools)

Le sezioni seguenti descrivono gli strumenti nativi di Azure disponibili per eseguire o supportare la migrazione. Per informazioni sulla scelta degli strumenti appropriati per supportare le attività di migrazione, vedere la [Guida alle decisioni relative agli strumenti di migrazione di Cloud Adoption Framework](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate offre un'esperienza di migrazione unificata ed estendibile. Azure Migrate offre un'esperienza centralizzata e dedicata per tenere traccia del percorso di migrazione nelle fasi di valutazione e migrazione ad Azure. Offre la possibilità di usare gli strumenti di propria scelta e di tenere traccia dell'avanzamento della migrazione tra questi strumenti.

Azure Migrate fornisce le funzionalità seguenti:

1. Funzionalità avanzate per valutazione e migrazione:
    - Valutazioni di Hyper-V.
    - Valutazione VMware: funzionalità migliorata.
    - Migrazione senza agente delle macchine virtuali VMware ad Azure.
1. Valutazione unificata, migrazione e rilevamento dell'avanzamento.
1. Approccio estendibile con integrazione di strumenti ISV (ad esempio Cloudamize).

Per eseguire una migrazione usando Azure Migrate, seguire questa procedura:

1. Cercare Azure Migrate in **Tutti i servizi**. Selezionare **Azure Migrate** per continuare.
1. Selezionare **Aggiungi uno strumento** per avviare il progetto di migrazione.
1. Selezionare la sottoscrizione, il gruppo di risorse e la geografia per ospitare la migrazione.
1. Selezionare **Selezionare lo strumento di valutazione** > **Azure Migrate: Valutazione server** >  **Avanti**.
1. Selezionare **Rivedi e aggiungi strumenti** e verificare la configurazione. Fare clic su **Aggiungi strumenti** per avviare il processo per creare il progetto di migrazione e registrare le soluzioni selezionate.

<!-- TODO: TBA -->

### <a name="read-more"></a>Altre informazioni

- [Esercitazione di Azure Migrate - Eseguire la migrazione di server fisici o virtuali ad Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)

## <a name="azure-site-recovery"></a>Azure Site Recovery

Il servizio Azure Site Recovery è in grado di gestire la migrazione delle risorse locali in Azure. È inoltre in grado di gestire e orchestrare il ripristino di emergenza di computer locali e VM di Azure per scopi legati alla continuità aziendale e ripristino di emergenza (BCDR).

La procedura seguente illustra il processo d'uso di Site Recovery per eseguire la migrazione:

> [!TIP]
> A seconda dello scenario, la procedura potrebbe essere leggermente diversa. Per altre informazioni, vedere l'articolo [Eseguire la migrazione dei computer locali ad Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure).

### <a name="prepare-azure-site-recovery-service"></a>Preparare il servizio Azure Site Recovery

1. Nella portale di Azure selezionare **+Crea una risorsa > Strumenti di gestione > Backup e Site Recovery**.
1. Se non è ancora stato creato un insieme di credenziali di ripristino, completare la procedura guidata per creare una risorsa dell'**insieme di credenziali di Servizi di ripristino**.
1. Nel menu **Risorsa** selezionare **Site Recovery > Preparare l'infrastruttura > Obiettivo di protezione**.
1. In **Protection goal** (Obiettivo di protezione) selezionare ciò che si intende migrare.
    1. **VMware:** Selezionare **In Azure > Sì, con VMware vSphere Hypervisor**.
    1. **Computer fisico:** Selezionare **In Azure > Non virtualizzato/Altro**.
    1. **Hyper-V:** Selezionare **In Azure > Sì, con Hyper-V**. Se le macchine virtuali Hyper-V sono gestite da VMM, selezionare **Sì**.

### <a name="configure-migration-settings"></a>Configurare le impostazioni di migrazione

1. Configurare l'ambiente di origine in modo appropriato.
1. Configurare l'ambiente di destinazione.
    1. Fare clic su **Preparare l'infrastruttura > Destinazione** e selezionare la sottoscrizione di Azure da usare.
    1. Specificare il modello di distribuzione di Gestione risorse.
    1. Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.
1. Configurare criteri di replica.
1. Abilitare la replica.
1. Eseguire una migrazione di test (failover di test).

### <a name="migrate-to-azure-using-failover"></a>Eseguire la migrazione ad Azure con failover

1. In **Impostazioni > Elementi replicati** selezionare il computer > **Failover**.
1. In **Failover** selezionare un **Punto di ripristino** in cui eseguire il failover. Selezionare l'ultimo punto di ripristino.
1. Configurare qualsiasi impostazioni della chiave di crittografia come richiesto.
1. Selezionare **Arrestare la macchina prima di iniziare il failover**. Site Recovery proverà ad arrestare le macchine virtuali prima di attivare il failover. Il failover continua anche se l'arresto ha esito negativo. Nella pagina Processi è possibile seguire lo stato del failover.
1. Assicurarsi che la macchina virtuale di Azure sia visualizzata in Azure come previsto.
1. In **Elementi replicati** fare clic con il pulsante destro del mouse sulla macchina virtuale e scegliere **Completa la migrazione**.
1. Eseguire tutta la procedura successiva alla migrazione come richiesto (vedere le informazioni rilevanti in questa guida).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.RecoveryServices]" submitText="Create a Recovery Services vault" :::

::: zone-end

::: zone target="docs"

Per altre informazioni, vedere:

- [Eseguire la migrazione di computer locali ad Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure)

::: zone-end

## <a name="azure-database-migration-service"></a>Servizio Migrazione del database di Azure

Il Servizio Migrazione del database di Azure è un servizio completamente gestito che consente migrazioni senza interruzioni da più origini di database alle piattaforme di dati di Azure, con tempi di inattività minimi (migrazioni online). Il Servizio Migrazione del database di Azure esegue tutta la procedura necessaria. È possibile avviare i progetti di migrazione con la garanzia che il processo si avvalga delle procedure consigliate da Microsoft.

### <a name="create-an-azure-database-migration-service-instance"></a>Creare un'istanza del Servizio Migrazione del database di Azure

Se è la prima volta che si usa il Servizio Migrazione del database di Azure è necessario registrare il provider di risorse per la sottoscrizione di Azure:

1. Selezionare **Tutti i servizi**, quindi **Sottoscrizioni** e scegliere la sottoscrizione di destinazione.
1. Selezionare **Provider di risorse**.
1. Cercare `migration` e quindi, a destra di **Microsoft.DataMigration**, selezionare **Registra**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

::: zone-end

Dopo aver registrato il provider di risorse, è possibile creare un'istanza del Servizio Migrazione del database di Azure.

1. Selezionare **+Crea una risorsa** e cercare nel marketplace il **Servizio Migrazione del database di Azure**.
1. Completare la procedura guidata di **Crea servizio Migrazione** e selezionare **Crea**.

Il servizio è ora pronto per eseguire la migrazione dei database di origine supportati, ad esempio SQL Server, MySQL, PostgreSQL o MongoDb.

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.AzureDMS]" submitText="Create an Azure Database Migration Service instance" :::

::: zone-end

::: zone target="docs"

Per altre informazioni, vedere:

- [Panoramica del Servizio Migrazione del database di Azure](https://docs.microsoft.com/azure/dms/dms-overview)
- [Creare un'istanza del Servizio Migrazione del database di Azure](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal)
- [Azure Migrate nel portale di Azure](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade)
- [Portale di Azure: Creare un progetto di migrazione](https://portal.azure.com/#create/Microsoft.AzureMigrate)

::: zone-end

## <a name="data-migration-assistant"></a>Data Migration Assistant

Data Migration Assistant (DMA) consente di eseguire l'aggiornamento a una piattaforma dati moderna individuando i problemi di compatibilità che possono influire sulle funzionalità del database nella nuova versione di SQL Server o in Database SQL di Azure. DMA consiglia miglioramenti per le prestazioni e l'affidabilità per l'ambiente di destinazione e consente di spostare lo schema, i dati e gli oggetti non contenuti dal server di origine al server di destinazione.

> [!NOTE]
> Per migrazioni di grandi dimensioni, in termini di numero e dimensione dei database, è consigliabile usare il Servizio Migrazione del database di Azure, che consente di eseguire la migrazione dei database su larga scala.
>

Per iniziare a usare Data Migration Assistant seguire la procedura seguente.

1. Scarica e installa Data Migration Assistant dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53595).
1. Per creare una valutazione, fare clic sull'icona **Nuovo (+)** e selezionare il tipo di progetto di **Valutazione**.
1. Impostare il tipo di server di origine e destinazione. Fare clic su **Create**(Crea).
1. Configurare le opzioni di valutazione in base alle esigenze (consigliare tutte le impostazioni predefinite).
1. Aggiungere i database da valutare.
1. Fare clic su **Next** (Avanti) per avviare la valutazione.
1. Visualizzare i risultati nel set di strumenti Data Migration Assistant.

È consigliabile, da parte dell'azienda, seguire l'approccio descritto in [Valutare un'azienda e consolidare i report di valutazione con DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports) per valutare più server, combinare i report e quindi usare i report Power BI forniti per analizzare risultati.

Per altre informazioni, inclusi i passaggi dettagliati sull'uso, vedere:

- [Panoramica di Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview)
- [Valutare un'azienda e consolidare i report di valutazione con DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports)
- [Analizzare i report di valutazione consolidati creati da Data Migration Assistant con Power BI](https://docs.microsoft.com/sql/dma/dma-powerbiassesreport)

## <a name="sql-server-migration-assistant"></a>SQL Server Migration Assistant

Microsoft SQL Server Migration Assistant (SSMA) è uno strumento progettato per automatizzare la migrazione del database a SQL Server da Microsoft Access, DB2, MySQL, Oracle e SAP ASE. Il concetto generale prevede la raccolta, la valutazione e la revisione con questi strumenti, tuttavia, a causa delle varianze del processo per ogni sistema di origine, si consiglia di esaminare la [documentazione dettagliata su SQL Server Migration Assistant](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant).

Per altre informazioni, vedere:

- [Panoramica di SQL Server Migration Assistant](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant)

## <a name="database-experimentation-assistant"></a>Database Experimentation Assistant

Database Experimentation Assistant (DEA) è una nuova soluzione di test A/B per gli aggiornamenti di SQL Server. Assiste nella valutazione di una versione di destinazione di SQL per un determinato carico di lavoro. I clienti che eseguono l'aggiornamento da versioni precedenti di SQL Server (SQL Server 2005 e versioni successive) a qualsiasi nuova versione di SQL Server, possono usare queste metriche di analisi.

Database Experimentation Assistant contiene le attività del flusso di lavoro seguenti:

- **Acquisisci:** Il primo passaggio del test A/B di SQL Server consiste nell'acquisire una traccia nel server di origine. Il server di origine è in genere il server di produzione.
- **Riproduci**: Il secondo passaggio del test A/B di SQL Server consiste nel riprodurre il file di traccia acquisito nei server di destinazione. Quindi, raccoglierà tracce estese dalle repliche per l'analisi.
- **Analisi:** Il passaggio finale consiste nel generare un report di analisi con le tracce di riproduzione. Il report di analisi può essere utile per ottenere informazioni sulle implicazioni della modifica proposta in termini di prestazioni.

Per altre informazioni, vedere:

- [Panoramica di Database Experimentation Assistant](https://docs.microsoft.com/sql/dea/database-experimentation-assistant-overview)

## <a name="cosmos-db-data-migration-tool"></a>Utilità di migrazione dati di Cosmos DB

L'utilità di migrazione dati di Azure Cosmos DB consente di importare dati da diverse origini nelle raccolte e nelle tabelle di Azure Cosmos DB. È possibile importare da file JSON, file CSV, SQL, MongoDB, archiviazione tabelle di Azure, Amazon DynamoDB e anche da raccolte di API SQL per Azure Cosmos DB. L'utilità di migrazione dati può essere usata anche per la migrazione da una raccolta con singola partizione a una raccolta con più partizioni per l'API SQL.

Per altre informazioni, vedere:

- [Utilità di migrazione dati di Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/import-data)

# <a name="third-party-migration-toolstabthird-party-tools"></a>[Strumenti di migrazione di terze parti](#tab/third-party-tools)

Esistono diversi strumenti di migrazione di terze parti e servizi ISV utili per il processo di migrazione. Ognuno offre diversi vantaggi e punti di forza. Questi strumenti comprendono:

## <a name="cloudamize"></a>Cloudamize

Cloudamize è un servizio ISV che copre tutte le fasi della strategia di migrazione.

[Altre informazioni](https://www.cloudamize.com)

## <a name="zerto"></a>Zerto

Zerto fornisce la replica virtuale per la gestione di ambienti Microsoft Hyper-V e VMware vSphere.

[Altre informazioni](https://www.zerto.com/solutions/use-cases/data-center-migration-software)

## <a name="carbonite"></a>Carbonite

Carbonite offre soluzioni di migrazione dei dati e dei server per eseguire la migrazione di carichi di lavoro a, da o tra qualsiasi ambiente fisico, virtuale o basato sul cloud.

[Altre informazioni](https://www.carbonite.com/data-protection/data-migration-software)

## <a name="movere"></a>Movere

Movere è una soluzione di individuazione che fornisce i dati e le informazioni necessarie per pianificare le migrazioni cloud e ottimizzare, monitorare e analizzare in modo continuo gli ambienti IT con massima affidabilità.

[Altre informazioni](https://www.movere.io)

## <a name="cosmos-db-partners"></a>Partner di Cosmos DB

È possibile scegliere tra un'ampia varietà di strumenti e partner esperti in integrazione di sistemi per supportare le migrazioni ad Azure Cosmos DB per specifici requisiti di database NoSQL.

[Altre informazioni](https://docs.microsoft.com/en-us/azure/cosmos-db/partners-migration-cosmosdb#migration-tools)

Visita il [Centro migrazione di Azure](https://azure.microsoft.com/migration/support) per scoprire le organizzazioni che offrono soluzioni tecnologiche partner pronte per l'uso, per adattarle agli scenari di migrazione, e per altre informazioni sugli strumenti aggiuntivi per la migrazione di terze parti e sui servizi di supporto.

Per visualizzare la gamma di opzioni disponibili per la migrazione di database e per le istruzioni dettagliate per le soluzioni native e dei partner, vedere la [Guida alla migrazione di database Azure](https://datamigration.microsoft.com).

# <a name="project-management-toolstabproject-management-tools"></a>[Strumenti di gestione dei progetti](#tab/project-management-tools)

I progetti che non vengono rilevati e gestiti hanno più probabilità che si verifichino problemi. Per garantire un esito positivo, è importante usare uno strumento di gestione dei progetti. Sono disponibili molti strumenti diversi; i project manager dell'organizzazione potrebbero averne già uno preferito.

Azure DevOps è lo strumento consigliato per la gestione di progetti durante la migrazione al cloud. Per accelerare l'utilizzo di Azure DevOps, Cloud Adoption Framework include uno strumento per la distribuzione automatica di un modello di progetto. Questo modello include le attività comuni eseguite durante un progetto di migrazione. Distribuire il modello seguendo [queste istruzioni](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/template). È quindi possibile modificarlo in base agli specifici [carichi di lavoro](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/workloads) e [asset](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/assets) di cui eseguire la migrazione.

Microsoft offre anche gli strumenti seguenti per la gestione dei progetti, che possono essere usati insieme per fornire funzionalità più ampie:

- [Microsoft Planner](https://tasks.office.com): Un semplice strumento visivo per organizzare il lavoro di squadra.
- [Microsoft Project](https://products.office.com/project/project-and-portfolio-management-software): Project and Portfolio Management, Resource Capacity Management, Financial Management, Timesheet and Schedule Management.
- [Microsoft Teams](https://products.office.com/microsoft-teams): Strumento di collaborazione e comunicazione del team. Teams consente inoltre di integrare Planner e altri strumenti per migliorare la collaborazione.
- [Azure DevOps](https://dev.azure.com): Il modello di pianificazione di Cloud Adoption Framework non è necessario per usare Azure DevOps. È possibile usare il servizio senza il modello per gestire l'infrastruttura come codice o usare gli elementi di lavoro e le lavagne per la gestione dei progetti. Crescendo, l'organizzazione potrà sfruttare le funzionalità CI/CD.

Questi non sono gli unici strumenti disponibili. Nella community di gestione dei progetti vengono ampiamente usati molti altri strumenti di terze parti.

## <a name="set-up-for-devops"></a>Configura per DevOps

Quando si esegue la migrazione nelle tecnologie cloud, si presenta una grande opportunità per la configurazione di DevOps e CI/CD nell'organizzazione. Anche se l'organizzazione gestisce solo l'infrastruttura, quando si inizia a gestire quest'ultima come codice usando i modelli e le procedure di settore per DevOps, è possibile iniziare ad aumentare l'agilità attraverso le pipeline CI/CD consentendo quindi l'adattamento a modifica, crescita, rilascio e persino a scenari di ripristino più rapidi.

[Azure DevOps](https://dev.azure.com) offre tutte le funzionalità necessarie e l'integrazione con Azure, in locale o persino in altri cloud. Per altre informazioni, [vedere](https://azure.microsoft.com/services/devops). Per un training guidato, vedere [CI and CD with Azure DevOps - Quickstart](https://microsoft.github.io/PartsUnlimited/pandp/200.1x-PandP-CICDQuickstartwithVSTS.html) (Avvio rapido: CI e CD con Azure DevOps).

# <a name="cost-managementtabmanagecost"></a>[Gestione costi](#tab/ManageCost)

Quando si esegue la migrazione delle risorse nell'ambiente cloud è importante eseguire un'analisi periodica dei costi. Questo consente di evitare addebiti imprevisti per l'utilizzo, poiché il processo di migrazione può richiedere requisiti di utilizzo aggiuntivi nei servizi. È anche possibile ridimensionare le risorse in base alle esigenze per bilanciare i costi e il carico di lavoro; per informazioni dettagliate vedere la sezione **[Ottimizzazione e trasformazione](./optimize-and-transform.md)** .
