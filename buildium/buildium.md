Open Rental Properties (Buildium)

<div>
  <button id="grid-btn">Grid View</button>
  <button id="list-btn">List View</button>
</div>

<div id="properties-container" style="display: flex; flex-wrap: wrap; gap: 16px;"></div>

<script>
async function fetchProperties() {
  try {
    const res = await fetch("https://yuxi-api.onrender.com/rental-property/sync-properties");
    const data = await res.json();

    const container = document.getElementById("properties-container");

    // Function to render cards
    function renderCards(layout = "grid") {
      container.innerHTML = ""; // clear existing

      data.properties.forEach(p => {
        const card = document.createElement("div");

        // Common styles
        card.style.border = "1px solid #ccc";
        card.style.borderRadius = "8px";
        card.style.padding = "10px";
        card.style.cursor = "pointer";
        card.style.boxShadow = "2px 2px 6px rgba(0,0,0,0.1)";
        card.onclick = () => window.open("./rented_property3/rented_property3.html", "_blank");

        // Layout-specific styles
        if(layout === "grid") {
          card.style.width = "200px";
          card.style.textAlign = "center";
        } else if(layout === "list") {
          card.style.display = "flex";
          card.style.alignItems = "center";
          card.style.width = "100%";
        }

        // Image
        const img = document.createElement("img");
        img.src = p.imageUrl;
        img.alt = p.title;
        img.style.borderRadius = "4px";
        img.style.marginBottom = layout === "grid" ? "8px" : "0";
        if(layout === "list") {
          img.style.width = "120px";
          img.style.height = "80px";
          img.style.objectFit = "cover";
          img.style.marginRight = "16px";
        } else {
          img.style.width = "100%";
        }

        // Title
        const title = document.createElement("h3");
        title.textContent = p.title;
        title.style.fontSize = "16px";
        title.style.margin = layout === "grid" ? "5px 0" : "0 0 4px 0";

        // Units + city
        const info = document.createElement("p");
        info.textContent = `${p.units} units in ${p.city}`;
        info.style.fontSize = "14px";
        info.style.margin = "0";

        // Append elements
        if(layout === "grid") {
          card.appendChild(img);
          card.appendChild(title);
          card.appendChild(info);
        } else {
          const textWrapper = document.createElement("div");
          textWrapper.appendChild(title);
          textWrapper.appendChild(info);
          card.appendChild(img);
          card.appendChild(textWrapper);
        }

        container.appendChild(card);
      });
    }

    // Initial render (grid)
    renderCards("grid");

    // Button listeners
    document.getElementById("grid-btn").onclick = () => renderCards("grid");
    document.getElementById("list-btn").onclick = () => renderCards("list");

  } catch (err) {
    console.error("Error fetching properties:", err);
  }
}

// Run the function
fetchProperties();
</script>