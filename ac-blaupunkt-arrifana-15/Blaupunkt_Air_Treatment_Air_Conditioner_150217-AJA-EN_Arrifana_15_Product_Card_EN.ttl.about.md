## Blaupunkt Air Treatment Air Conditioner 150217-AJA-EN Arrifana 15 Product Card

<https://chatgpt.com/share/684f2272-8e38-8007-a2bc-2f66102a9c83>

<https://chatgpt.com/c/684f1e74-f93c-8007-8353-bdc3b31277fa>

In this proposal, we model the **Arrifana 15** air conditioner using a combination of established ontologies to ensure interoperability and semantic richness. We adopt **GoodRelations** for core product structuring ([en.wikipedia.org][1]), **QUDT** for precise quantity and unit modeling ([qudt.org][2], [qudt.org][3]), **GS1 Ontology** for global trade item numbering (EAN/GTIN) ([ref.gs1.org][4]), and **Schema.org** for general properties and warranty semantics via **WarrantyPromise** ([schema.org][5]). These vocabularies are widely adopted and available in Turtle format ([schema.org][6]).

## Ontology Selection and Design

### GoodRelations

* **Purpose**: Modeling products, services, and offerings in e-commerce.
* **Key Classes/Properties**:

  * `gr:ProductOrServiceModel` for product models (our Arrifana 15)
  * `gr:name`, `gr:hasBrand`, `gr:hasEAN_UCC13` for basic identification ([en.wikipedia.org][1])
* **Integration**: Incorporated into Schema.org in 2012 for search-engine friendliness ([heppnetz.de][7])

### QUDT (Quantity, Unit, Dimension & Type)

* **Purpose**: Precise representation of numeric values with units.
* **Key Classes/Properties**:

  * `qudt:QuantityValue` to bundle a numeric value and a unit
  * Unit vocabularies (e.g., `unit:KiloWatt`, `unit:DegreeCelsius`) ([qudt.org][2])
* **Pattern**: Each measurement (e.g., power, dimensions, flow) is an instance of `qudt:QuantityValue` ([qudt.org][3])

### GS1 Ontology

* **Purpose**: Standardized GTIN/EAN and supply-chain identifiers.
* **Key Classes/Properties**:

  * `gs1:hasGTIN13` (or Schema.org’s `schema:gtin13`) for EANs ([ref.gs1.org][4])

### Schema.org

* **Purpose**: Broad web vocabulary for products, structured data, and warranties.
* **Key Classes/Properties**:

  * `schema:Product` as super-class
  * `schema:productID`, `schema:mpn`, `schema:brand`, `schema:gtin13`
  * `schema:WarrantyPromise` for warranty details (duration as ISO 8601) ([schema.org][5], [schema.org][6])

## Turtle Representation

The following Turtle snippet uses the prefixes and modeling patterns described above ([schema.org][6], [en.wikipedia.org][1]):

```turtle
@prefix ex:     <http://example.org/vocab/> .
@prefix schema: <http://schema.org/> .
@prefix gr:     <http://purl.org/goodrelations/v1#> .
@prefix qudt:   <http://qudt.org/schema/qudt/> .
@prefix unit:   <http://qudt.org/vocab/unit/> .
@prefix gs1:    <http://purl.org/gs1/voc/> .
@prefix xsd:    <http://www.w3.org/2001/XMLSchema#> .

# The Arrifana 15 product model
ex:Arrifana15
    a               gr:ProductOrServiceModel ;
    gr:name         "Arrifana 15" ;
    gr:hasBrand     "Blaupunkt" ;
    schema:category "Air Conditioner" ;
    schema:productID "150217-AJA-EN" ;
    schema:mpn      "BAC-PO-0015-C06D" ;
    schema:gtin13   "5902596575687" ;

    # Cooling power in both kW and kBTU
    ex:coolingPower ex:coolingPowerKW, ex:coolingPowerBTU ;

    # Energy efficiency
    ex:eer         "2.62"^^xsd:decimal ;
    ex:euEnergyEfficiencyCategory "A" ;

    # Dehumidification, reservoir, circulation
    ex:dehumidification [
        a qudt:QuantityValue ;
        qudt:value "80"^^xsd:decimal ;
        qudt:unit unit:LitrePerDay
    ] ;
    ex:waterReservoir [
        a qudt:QuantityValue ;
        qudt:value "4"^^xsd:decimal ;
        qudt:unit unit:Litre
    ] ;
    ex:airCirculation [
        a qudt:QuantityValue ;
        qudt:value "450"^^xsd:decimal ;
        qudt:unit unit:CubicMetrePerHour
    ] ;

    # Sound levels
    ex:soundLevelMin "52"^^xsd:decimal ;
    ex:soundLevelMid "54"^^xsd:decimal ;
    ex:soundLevelMax "56"^^xsd:decimal ;

    # Thermostat range
    ex:thermostatMin [
        a qudt:QuantityValue ;
        qudt:value "18"^^xsd:decimal ;
        qudt:unit unit:DegreeCelsius
    ] ;
    ex:thermostatMax [
        a qudt:QuantityValue ;
        qudt:value "35"^^xsd:decimal ;
        qudt:unit unit:DegreeCelsius
    ] ;

    # Electrical specs
    ex:powerSupplyVoltage [
        a qudt:QuantityValue ;
        qudt:value "220"^^xsd:decimal ;
        qudt:unit unit:Volt
    ], [
        a qudt:QuantityValue ;
        qudt:value "240"^^xsd:decimal ;
        qudt:unit unit:Volt
    ] ;
    ex:powerSupplyFrequency [
        a qudt:QuantityValue ;
        qudt:value "50"^^xsd:decimal ;
        qudt:unit unit:Hertz
    ] ;
    ex:powerSupplyPhase "1"^^xsd:integer ;

    ex:powerConsumption [
        a qudt:QuantityValue ;
        qudt:value "1680"^^xsd:decimal ;
        qudt:unit unit:Watt
    ] ;
    ex:operatingCurrent [
        a qudt:QuantityValue ;
        qudt:value "7.5"^^xsd:decimal ;
        qudt:unit unit:Ampere
    ] ;

    # Net dimensions
    ex:widthNet [
        a qudt:QuantityValue ;
        qudt:value "365"^^xsd:decimal ;
        qudt:unit unit:Millimetre
    ] ;
    ex:heightNet [
        a qudt:QuantityValue ;
        qudt:value "775"^^xsd:decimal ;
        qudt:unit unit:Millimetre
    ] ;
    ex:depthNet [
        a qudt:QuantityValue ;
        qudt:value "568"^^xsd:decimal ;
        qudt:unit unit:Millimetre
    ] ;

    # Shipping dimensions
    ex:widthShip [
        a qudt:QuantityValue ;
        qudt:value "445"^^xsd:decimal ;
        qudt:unit unit:Millimetre
    ] ;
    ex:heightShip [
        a qudt:QuantityValue ;
        qudt:value "875"^^xsd:decimal ;
        qudt:unit unit:Millimetre
    ] ;
    ex:depthShip [
        a qudt:QuantityValue ;
        qudt:value "735"^^xsd:decimal ;
        qudt:unit unit:Millimetre
    ] ;

    # Weight
    ex:netWeight [
        a qudt:QuantityValue ;
        qudt:value "40"^^xsd:decimal ;
        qudt:unit unit:Kilogram
    ] ;
    ex:grossWeight [
        a qudt:QuantityValue ;
        qudt:value "51"^^xsd:decimal ;
        qudt:unit unit:Kilogram
    ] ;

    # Connections
    ex:outletPipeDiameter [
        a qudt:QuantityValue ;
        qudt:value "150"^^xsd:decimal ;
        qudt:unit unit:Millimetre
    ] ;
    ex:outletPipeLength [
        a qudt:QuantityValue ;
        qudt:value "1500"^^xsd:decimal ;
        qudt:unit unit:Millimetre
    ] ;

    # Application area as a list of values
    ex:applicationArea [
        a qudt:QuantityValue ;
        qudt:value "25"^^xsd:decimal ;
        qudt:unit unit:SquareMetre
    ], [
        a qudt:QuantityValue ;
        qudt:value "30"^^xsd:decimal ;
        qudt:unit unit:SquareMetre
    ], [
        a qudt:QuantityValue ;
        qudt:value "35"^^xsd:decimal ;
        qudt:unit unit:SquareMetre
    ] ;

    # Warranty
    schema:warrantyPromise [
        a schema:WarrantyPromise ;
        schema:duration "P3Y"^^xsd:duration
    ] .

# Instances for dual-unit cooling power
ex:coolingPowerKW
    a qudt:QuantityValue ;
    qudt:value "4.4"^^xsd:decimal ;
    qudt:unit unit:KiloWatt .

ex:coolingPowerBTU
    a qudt:QuantityValue ;
    qudt:value "15"^^xsd:decimal ;
    qudt:unit unit:BritishThermalUnit .
```

This Turtle representation leverages the strengths of each ontology for a clean, ergonomic, and machine-readable model of the technical specifications.

[1]: https://en.wikipedia.org/wiki/GoodRelations?utm_source=chatgpt.com "GoodRelations"
[2]: https://www.qudt.org/doc/DOC_SCHEMA-QUDT.html?utm_source=chatgpt.com "Quantities, Units, Dimensions and Types (QUDT) Schema"
[3]: https://qudt.org/schema/qudt/QuantityValue?utm_source=chatgpt.com "qudt:QuantityValue"
[4]: https://ref.gs1.org/docs/2014/gtin-plus-on-the-web/GTINplusOTW-GS1OntologyDraftStandardSpecification?utm_source=chatgpt.com "[PDF] GTIN+ OTW GS1 Ontology Draft Standard Specification"
[5]: https://schema.org/WarrantyPromise?utm_source=chatgpt.com "WarrantyPromise - Schema.org Type"
[6]: https://schema.org/version/latest?utm_source=chatgpt.com "Schema.org Version 29.2"
[7]: https://www.heppnetz.de/ontologies/goodrelations/v1.html?utm_source=chatgpt.com "GoodRelations Language Reference - Martin Hepp"

