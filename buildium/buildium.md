Open Rental Properties (Buildium)

[Picture1]

Related Data 

[Rent this property](./rented_property1/rented_property1.md)

[Picture2]

Related Data 

[Rent this property](./rented_property2/rented_property2.md)

[Picture3]

Related Data 

[Rent this property](./rented_property3/rented_property3.md)

[⬅ Back](../index.md)

<div id="json-output"></div>

<script>
async function fetchProperties() {
  try {
    const res = await fetch("https://yuxi-api.onrender.com/rental-property/sync-properties");
    const data = await res.json();

    document.getElementById("json-output").textContent = JSON.stringify(data, null, 2);
  } catch (err) {
    console.error("Error fetching properties:", err);
  }
}

fetchProperties();
</script>