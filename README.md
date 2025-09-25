# Dashboard-MVP3
.getElementById("jobScope").value,
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
