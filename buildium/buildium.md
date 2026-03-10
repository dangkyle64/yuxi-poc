Open Rental Properties (Buildium)

<div id="properties-container" style="display: flex; flex-wrap: wrap; gap: 20px;"></div>

<script>
async function fetchProperties() {
  try {
    const res = await fetch("https://yuxi-api.onrender.com/rental-property/sync-properties");
    const data = await res.json();

    console.log(data)
    
    const container = document.getElementById("properties-container");

    data.properties.forEach(p => {
      // Create the card wrapper
      const card = document.createElement("div");
      card.style.border = "1px solid #ccc";
      card.style.borderRadius = "8px";
      card.style.padding = "10px";
      card.style.width = "200px";
      card.style.boxShadow = "2px 2px 6px rgba(0,0,0,0.1)";
      card.style.textAlign = "center";
      card.style.cursor = "pointer";

      // Make card clickable to Buildium link
      // p.buildiumUrl for when each card has own link temp all same link
      card.onclick = () => window.open("./rented_property3/rented_property3.html", "_blank");

      // Image
      const img = document.createElement("img");
      img.src = p.imageUrl;
      img.alt = p.title;
      img.style.width = "100%";
      img.style.borderRadius = "4px";
      img.style.marginBottom = "8px";

      // Title
      const title = document.createElement("h3");
      title.textContent = p.title;
      title.style.fontSize = "16px";
      title.style.margin = "5px 0";

      // Units + city
      const info = document.createElement("p");
      info.textContent = `${p.units} units in ${p.city}`;
      info.style.fontSize = "14px";
      info.style.margin = "0";

      // Append elements to the card
      card.appendChild(img);
      card.appendChild(title);
      card.appendChild(info);

      // Append card to container
      container.appendChild(card);
    });
  } catch (err) {
    console.error("Error fetching properties:", err);
  }
}

// Run the function
fetchProperties();
</script>