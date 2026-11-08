
let schedules = JSON.parse(
  localStorage.getItem("mediSchedules") || "[]"
);

let notified = [];

function clock() {
  document.getElementById("clock").textContent =
    new Date().toLocaleString("id-ID");
}

setInterval(clock, 1000);
clock();

function saveMedicine() {
  const patient = document.getElementById("patient").value.trim();
  const medicine = document.getElementById("medicine").value.trim();
  const dose = document.getElementById("dose").value.trim();
  const time = document.getElementById("time").value;

  if (!patient || !medicine || !dose || !time) {
    alert("Silakan lengkapi semua data.");
    return;
  }

  schedules.push({ patient, medicine, dose, time });

  localStorage.setItem(
    "mediSchedules",
    JSON.stringify(schedules)
  );

  render();
  alert("Jadwal obat berhasil disimpan.");
}

function render() {
  const box = document.getElementById("schedule");

  if (!schedules.length) {
    box.textContent = "Belum ada jadwal obat.";
    return;
  }

  box.innerHTML = schedules.map((item, index) => `
    <div class="medicine-card">
      <h3>${escapeHTML(item.medicine)}</h3>
      <p>Pasien: ${escapeHTML(item.patient)}</p>
      <p>Dosis: ${escapeHTML(item.dose)}</p>
      <p>Jam: ${escapeHTML(item.time)}</p>
      <button onclick="removeSchedule(${index})">
        Hapus Jadwal
      </button>
    </div>
  `).join("");
}

function escapeHTML(value) {
  return String(value).replace(/[&<>"']/g, c => ({
    "&": "&amp;",
    "<": "&lt;",
    ">": "&gt;",
    '"': "&quot;",
    "'": "&#39;"
  })[c]);
}

function removeSchedule(index) {
  schedules.splice(index, 1);
  localStorage.setItem(
    "mediSchedules",
    JSON.stringify(schedules)
  );
  render();
}

async function requestAlarmPermission() {
  if ("Notification" in window &&
      Notification.permission === "default") {
    await Notification.requestPermission();
  }
}

function checkAlarm() {
  if (!("Notification" in window) ||
      Notification.permission !== "granted") return;

  const now = new Date();
  const currentTime =
    String(now.getHours()).padStart(2, "0") + ":" +
    String(now.getMinutes()).padStart(2, "0");

  schedules.forEach((item, index) => {
    const key = now.toDateString() + "-" + index;

    if (item.time === currentTime &&
        !notified.includes(key)) {
      notified.push(key);

      new Notification("MEDI ALARM", {
        body: "Waktunya minum " + item.medicine +
              " (" + item.dose + ")"
      });
    }
  });
}

setInterval(checkAlarm, 10000);
render();
requestAlarmPermission();
