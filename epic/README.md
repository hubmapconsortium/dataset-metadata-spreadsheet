# Header Attributes Specification

This README document explains the attributes in the header of EPIC data tables. Data curators should use these attributes to give data providers the guidelines for completing each column.

## Attributes

* **Type** _(required)_

  The type defines the kind of data that a variable can hold. Common types include integer, string, float, boolean, date, and more. The type determines what kind of operations and validations can be applied to the variable.

  Permissible values: `text` | `integer` | `float` | `doi` | `boolean` | `obo id`

* **Unit**

  The unit of measurement for the data values.

  Permissible values: `pixel` | `square micrometer`

* **Feature class** _(required)_

  The the type of feature. For example, the feature could be ontology-related, describe morphology, refer to an antibody, and so on. There is a predefined set of feature classes. If you are including a type of feature not relevant to one of the existing feature classes, please contact [HuBMAP Help](mailto:help@hubmapconsortium.org).

  Permissible values: `gene` | `neighborhood` | `mask` | `spatial` | `morphology` | `ontology` | `antibody` | `IMS`

* **Description** _(required)_

  The description provides a detailed explanation of what the variable represents and how it should be used. It helps users understand the purpose and context of the variable within the dataset.

* **Protocol used to derive this feature value (DOI)**

  This field contains a DOI pointing to the protocol that describes the steps used to define this feature variable. If the feature is an antibody, this would be the protocol defining the spatial assay used. This is different from the object-specific protocol that was used to identify and mask the object.

* **Alternative ID**

  The alternative ID provides the mean to store the standardized code about the feature variable. For example, if the feature variable is about antibodies, the it should be filled with an RRID code, genes should be an HGNC code, proteins should be a UniProt identifier, and lipids or metabolites should reference to Metabolomics Workbench.
  
* **Permissible values**

  Permissible values are a predefined set of allowed values for the variable. This is often used for categorical variables where only certain values are valid.

  Format: Use the pipe `|` symbol to separate between values.
  
  Example: "A | B | AB | O" (as permissible values for blood types)
  
* **Requirement level** _(required)_

  The requirement level indicates whether a variable is mandatory or optional. It specifies whether the variable must have a value (required) or if it can be left blank (optional).

  Permissible values: `REQUIRED` | `OPTIONAL`

## Validation

An online validator is available to validate the EPIC spreadsheet, both the header attributes and the data table.

```
curl --request POST \
  --url https://api.stage.metadatavalidator.metadatacenter.org/service/validate-structured-xlsx \
  --header 'Content-Type: multipart/form-data' \
  --form input_file=@/path/to/epic-spreadsheet.xlsx
```

**Caveat**: The validator only validates some header attributes such as "Type", "Permissible values" and "Requirement level".
