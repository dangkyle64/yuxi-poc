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

<ul id="properties-list"></ul>

<script>
async function fetchProperties() {
  try {
    const res = await fetch("https://https://yuxi-api.onrender.com//properties/sync-properties");
    const data = await res.json();
    console.log("Properties:", data);

    const list = document.getElementById("properties-list");
    data.properties.forEach(p => {
      const li = document.createElement("li");
      li.textContent = `${p.title} (${p.units} units in ${p.city})`;
      list.appendChild(li);
    });
  } catch (err) {
    console.error(err);
  }
}

fetchProperties();
</script>