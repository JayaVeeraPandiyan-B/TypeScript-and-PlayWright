DECLARE @Expected_Department     VARCHAR(100) = 'Global Corporate affairs'
DECLARE @Expected_SubDepartment  VARCHAR(100) = 'Corporate Communications'
DECLARE @Expected_Status         VARCHAR(50)  = 'Active'
DECLARE @Expected_Title          VARCHAR(100) = 'Associate Vice President'

SELECT
    full_name,
    CASE WHEN ISNULL(HR_DEPARTMENT, '') <> @Expected_Department
         THEN 'Department changed from [' + @Expected_Department + '] to [' + ISNULL(HR_DEPARTMENT, 'NULL') + ']' END AS Department_Change,
    CASE WHEN ISNULL(HR_SUBDEPARTMENT, '') <> @Expected_SubDepartment
         THEN 'Sub-Department changed from [' + @Expected_SubDepartment + '] to [' + ISNULL(HR_SUBDEPARTMENT, 'NULL') + ']' END AS SubDept_Change,
    CASE WHEN ISNULL(WD_FTE_Status, '') <> @Expected_Status
         THEN 'Status changed from [' + @Expected_Status + '] to [' + ISNULL(WD_FTE_Status, 'NULL') + ']' END AS Status_Change,
    CASE WHEN ISNULL(BUSINESS_TITLE, '') <> @Expected_Title
         THEN 'Title changed from [' + @Expected_Title + '] to [' + ISNULL(BUSINESS_TITLE, 'NULL') + ']' END AS Title_Change
FROM EDW20_QA.dbo.VW_IR_workers_consolidated
WHERE full_name = 'Zoe Esposito'
  AND (
       ISNULL(HR_DEPARTMENT, '') <> @Expected_Department
    OR ISNULL(HR_SUBDEPARTMENT, '') <> @Expected_SubDepartment
    OR ISNULL(WD_FTE_Status, '') <> @Expected_Status
    OR ISNULL(BUSINESS_TITLE, '') <> @Expected_Title
  )
