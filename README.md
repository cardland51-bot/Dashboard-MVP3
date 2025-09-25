# Dashboard-MVP3
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cardinal Landscaping Dashboard</title>
<style>
/* ---------- Base & Typography ---------- */
body {
    font-family: 'Inter', sans-serif;
    background: #f0f0f0;
    color: #333;
    margin: 0;
    padding: 0;
}
header {
    background: #B31B1B; 
    color: #fff;
    padding: 16px 20px;
    text-align: center;
    font-weight: 600;
    font-size: 1.5rem;
    box-shadow: 0 2px 10px rgba(0,0,0,0.2);
}

/* ---------- Container ---------- */
.container {
    display: flex;
    flex-wrap: wrap;
    padding: 16px;
    gap: 16px;
}

/* ---------- Sidebar ---------- */
.sidebar {
    width: 320px;
    background: rgba(255,255,255,0.85);
    border-radius: 16px;
    backdrop-filter: blur(12px);
    padding: 20px;
    flex-shrink: 0;
    transition: all 0.3s ease;
}

/* ---------- Buttons ---------- */
button.add-item, button[type="submit"] {
    width: 100%;
    padding: 12px;
    border-radius: 10px;
    border: none;
    cursor: pointer;
    font-weight: 600;
    font-size: 1rem;
    color: #fff;
    background: #B31B1B; 
    margin-bottom: 12px;
    transition: all 0.3s ease;
}
button.add-item:hover, button[type="submit"]:hover { filter: brightness(1.1); }

/* ---------- Inputs ---------- */
input, select, textarea {
    width: 100%;
    padding: 10px;
    margin-bottom: 12px;
    border-radius: 8px;
    border: 1px solid #ccc;
    font-size: 0.95rem;
}
textarea { resize: vertical; }

/* ---------- Main Content ---------- */
.main {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 16px;
}

/* ---------- Job List ---------- */
section.card {
    background: rgba(255,255,255,0.85);
    border-radius: 16px;
    backdrop-filter: blur(12px);
    padding: 20px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    max-height: 600px;
    overflow-y: auto;
}
section.card h2 {
    margin: 0 0 12px 0;
    font-size: 1.3rem;
    color: #B31B1B;
}
section.card ul {
    list-style: none;
    padding: 0;
    margin: 0;
}
section.card li {
    padding: 12px;
    border-radius: 12px;
    margin-bottom: 10px;
    border: 1px solid #ddd;
    background: rgba(255,255,255,0.7);
    display: flex;
    flex-direction: column;
    transition: all 0.25s ease;
    cursor: pointer;
}
section.card li:hover { background: rgba(255,255,255,0.9); }
.badge { font-weight: 600; font-size: 0.85rem; color:#fff; padding:2px 8px; border-radius:10px; display:inline-block; margin-bottom:4px; }
.badge.Upcoming { background: #FBBF24; }
.badge.Ongoing { background: #10B981; }
.badge.Completed { background: #6B7280; }

/* ---------- Responsive ---------- */
@media(max-width: 768px){
    .container { flex-direction: column; }
    .sidebar { width: 100%; order: 1; }
    .main { order: 2; }
    section.card { max-height: 350px; }
}
</style>
</head>
<body>

<header>Cardinal Landscaping Dashboard</header>

<div class="container">

  <div class="sidebar">
    <button class="add-item" onclick="toggleForm()">Add Job</button>

    <div id="addJobForm" style="display:none; margin-top:15px;">
      <form id="jobForm">
        <label>Contact Name: <input type="text" id="contactName"></label>
        <label>Phone Number: <input type="text" id="contactPhone"></label>
        <label>Address: <input type="text" id="jobAddress"></label>

        <!-- Mulch -->
        <label>Mulch: 
          <select id="mulchSelect">
            <option value="">No</option>
            <option value="Yes">Yes</option>
          </select>
        </label>
        <div id="mulchOptions" style="display:none; margin-left:10px;">
          <label>Mulch Color:
            <select id="mulchColor">
              <option value="Red">Red</option>
              <option value="Brown">Brown</option>
              <option value="Black">Black</option>
            </select>
          </label>
          <label>Mulch Amount:
            <select id="mulchAmount">
              <option value="1">Small (1 yd³)</option>
              <option value="3">Medium (3 yd³)</option>
              <option value="5+">Large (5+ yd³)</option>
            </select>
          </label>
        </div>

        <!-- Edging -->
        <label>Edging: 
          <select id="edgingSelect">
            <option value="">No</option>
            <option value="Yes">Yes</option>
          </select>
        </label>
        <div id="edgingOptions" style="display:none; margin-left:10px;">
          <label>Edging Type:
            <select id="edgingType">
              <option value="Plastic">Plastic</option>
              <option value="Metal">Metal</option>
              <option value="Earth">Earth</option>
            </select>
          </label>
        </div>

        <!-- Shrub Trimming -->
        <label>Shrub Trimming:
          <select id="shrubsSelect">
            <option value="">No</option>
            <option value="Yes">Yes</option>
          </select>
        </label>
        <div id="shrubsOptions" style="display:none; margin-left:10px;">
          <label>Number of Shrubs:
            <select id="shrubsNumber">
              <option value="Few">&lt;10</option>
              <option value="Many">10-20</option>
              <option value="A lot">&gt;35</option>
            </select>
          </label>
          <label>Shrubs over 10 ft?
            <select id="shrubsHeight">
              <option value="No">No</option>
              <option value="Yes">Yes</option>
            </select>
          </label>
        </div>

        <!-- Weeding -->
        <label>Weeding:
          <select id="weedingSelect">
            <option value="">No</option>
            <option value="Yes">Yes</option>
          </select>
        </label>
        <div id="weedingOptions" style="display:none; margin-left:10px;">
          <label>Status:
            <select id="weedingStatus">
              <option value="Light">Light</option>
              <option value="Moderate">Moderate</option>
              <option value="Heavy">Heavy</option>
            </select>
          </label>
        </div>

        <!-- Debris -->
        <label>Debris:
          <select id="debrisSelect">
            <option value="">None</option>
            <option value="Haul Off">Haul Off</option>
            <option value="Leave On Site">Leave On Site</option>
          </select>
        </label>

        <!-- Cleanup -->
        <label>Perennial Cleanup:
          <select id="perennialCleanup">
            <option value="">No</option>
            <option value="Yes">Yes</option>
          </select>
        </label>
        <label>Spring/Fall Cleanup:
          <select id="seasonalCleanup">
            <option value="">No</option>
            <option value="Yes">Yes</option>
          </select>
        </label>

        <!-- Scope -->
        <label>Scope / Additional Details:
          <textarea id="jobScope" rows="2"></textarea>
        </label>

        <!-- Job Status & Date -->
        <label>Job Status:
          <select id="jobStatus">
            <option value="Upcoming">Upcoming</option>
            <option value="Ongoing">Ongoing</option>
            <option value="Completed">Completed</option>
          </select>
        </label>
        <label>Expected Start Date: <input type="date" id="expectedDate"></label>

        <button type="submit">Save Job</button>
      </form>
    </div>
  </div>

  <div class="main">
    <section class="card">
      <h2>Jobs List</h2>
      <ul id="jobsList">Loading jobs...</ul>
    </section>
  </div>

</div>

<script>
const SHEET_URL = "YOUR_WEB_APP_URL_HERE";

// Toggle form
function toggleForm() {
  const f = document.getElementById("addJobForm");
  f.style.display = f.style.display === "none" ? "block" : "none";
}

// Show/hide dependent menus
["mulchSelect","edgingSelect","shrubsSelect","weedingSelect"].forEach(id=>{
  document.getElementById(id).addEventListener("change", e=>{
    document.getElementById(id.replace("Select","Options")).style.display = e.target.value === "Yes" ? "block" : "none";
  });
});

let jobs = [];
let editIndex = null;

// Render jobs
function renderJobs(){
  const ul = document.getElementById("jobsList");
  ul.innerHTML = "";
  if(jobs.length===0){ ul.innerHTML="<li>No jobs added yet</li>"; return; }
  jobs.forEach((job,idx)=>{
    const li = document.createElement("li");
    li.innerHTML = `<strong>${job.ContactName||"No Contact"}</strong> | ${job.Address||"No Address"}<br>
      Mulch: ${job.Mulch||"No"} ${job.Mulch==="Yes"?`(${job.MulchAmount} yd³, ${job.MulchColor})`:""}<br>
      Edging: ${job.Edging||"No"} ${job.EdgingType?`(${job.EdgingType})`:""}<br>
      Shrubs: ${job.Shrubs||"No"} ${job.Shrubs==="Yes"?`(${job.ShrubsNumber}, >10ft? ${job.ShrubsHeight})`:""}<br>
      Weeding: ${job.Weeding||"No"} ${job.Weeding==="Yes"?`(${job.WeedingStatus})`:""}<br>
      Debris: ${job.Debris||"None"}<br>
      Perennial: ${job.PerennialCleanup||"No"} | Spring/Fall: ${job.SeasonalCleanup||"No"}<br>
      Scope: ${job.JobScope||""}<br>
      Status: <span class="badge ${job.JobStatus}">${job.JobStatus}</span> | Expected: ${job.ExpectedDate||"N/A"}`;
    li.onclick=()=>editJob(idx);
    ul.appendChild(li);
  });
}

// Edit job
function editJob(idx){
  const job=jobs[idx];
  editIndex=idx;
  document.getElementById("addJobForm").style.display="block";
  document.getElementById("contactName").value=job.ContactName||"";
  document.getElementById("contactPhone").value=job.Phone||"";
  document.getElementById("jobAddress").value=job.Address||"";
  document.getElementById("mulchSelect").value=job.Mulch||"";
  document.getElementById("mulchOptions").style.display=job.Mulch==="Yes"?"block":"none";
  document.getElementById("mulchColor").value=job.MulchColor||"Red";
  document.getElementById("mulchAmount").value=job.MulchAmount||"1";
  document.getElementById("edgingSelect").value=job.Edging||"";
  document.getElementById("edgingOptions").style.display=job.Edging==="Yes"?"block":"none";
  document.getElementById("edgingType").value=job.EdgingType||"Plastic";
  document.getElementById("shrubsSelect").value=job.Shrubs||"";
  document.getElementById("shrubsOptions").style.display=job.Shrubs==="Yes"?"block":"none";
  document.getElementById("shrubsNumber").value=job.ShrubsNumber||"Few";
  document.getElementById("shrubsHeight").value=job.ShrubsHeight||"No";
  document.getElementById("weedingSelect").value=job.Weeding||"";
  document.getElementById("weedingOptions").style.display=job.Weeding==="Yes"?"block":"none";
  document.getElementById("weedingStatus").value=job.WeedingStatus||"Light";
  document.getElementById("debrisSelect").value=job.Debris||"";
  document.getElementById("perennialCleanup").value=job.PerennialCleanup||"";
  document.getElementById("seasonalCleanup").value=job.SeasonalCleanup||"";
  document.getElementById("jobScope").value=job.JobScope||"";
  document.getElementById("jobStatus").value=job.JobStatus||"Upcoming";
  document.getElementById("expectedDate").value=job.ExpectedDate||"";
}

// Load jobs from sheet
async function loadJobs(){
  try{
    const res=await fetch(SHEET_URL);
    jobs=await res.json();
    renderJobs();
  }catch(e){ console.error(e); }
}

// Save job to sheet
async function saveJob(job){
  try{
    await fetch(SHEET_URL,{method:'POST',body:JSON.stringify(job)});
    await loadJobs();
  }catch(e){ console.error(e); }
}

// Form submission
document.getElementById("jobForm").addEventListener("submit", async e=>{
  e.preventDefault();
  const job={
    ContactName: document.getElementById("contactName").value,
    Phone: document.getElementById("contactPhone").value,
    Address: document.getElementById("jobAddress").value,
    Mulch: document.getElementById("mulchSelect").value,
    MulchColor: document.getElementById("mulchColor").value,
    MulchAmount: document.getElementById("mulchAmount").value,
    Edging: document.getElementById("edgingSelect").value,
    EdgingType: document.getElementById("edgingType").value,
    Shrubs: document.getElementById("shrubsSelect").value,
    ShrubsNumber: document.getElementById("shrubsNumber").value,
    ShrubsHeight: document.getElementById("shrubsHeight").value,
    Weeding: document.getElementById("weedingSelect").value,
    WeedingStatus: document.getElementById("weedingStatus").value,
    Debris: document.getElementById("debrisSelect").value,
    PerennialCleanup: document.getElementById("perennialCleanup").value,
    SeasonalCleanup: document.getElementById("seasonalCleanup").value,
    JobScope: document.getElement.getElementById("jobScope").value,
    JobStatus: document.getElementById("jobStatus").value,
    ExpectedDate: document.getElementById("expectedDate").value
  };

  if(editIndex !== null){
    // Optional: include an "ID" field to update existing row in Google Sheets
    job.Index = editIndex;
    editIndex = null;
  }

  await saveJob(job);

  document.getElementById("jobForm").reset();
  // Hide optional menus
  ["mulchOptions","edgingOptions","shrubsOptions","weedingOptions"].forEach(id=>{
    document.getElementById(id).style.display="none";
  });
  // Collapse form
  document.getElementById("addJobForm").style.display="none";
});

loadJobs(); // initial load
</script>

</body>
</html>
