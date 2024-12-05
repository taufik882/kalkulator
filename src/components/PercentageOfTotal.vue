<template>
  <div>
    <h2>Persentase Jumlah</h2>
    <form @submit.prevent="calculate">
      <div class="form-group">
        <label for="nama">Nama:</label>
        <input v-model="nama" type="text" id="nama" required />
      </div>
      <div class="form-group">
        <label for="a">Nilai A:</label>
        <input v-model.number="a" type="number" id="a" required />
      </div>
      <div class="form-group">
        <label for="b">Nilai B (%):</label>
        <input v-model.number="b" type="number" id="b" required />
      </div>
      <button type="submit">Hitung</button>
    </form>

    <ResultTable :results="results" />
    <button @click="exportToPDF" class="export-btn">Export ke PDF</button>
  </div>
</template>

<script>
import ResultTable from './ResultTable.vue';
import { jsPDF } from 'jspdf';
import autoTable from 'jspdf-autotable';

export default {
  components: { ResultTable },
  data() {
    return {
      nama: '', // Tambahkan data untuk nama
      a: null,
      b: null,
      results: [], // Array untuk menyimpan semua hasil
    };
  },
  methods: {
    calculate() {
      const c = (this.a * this.b) / 100; // Hitung jumlah persentase
      const d = c - this.a; // Hitung selisih absolut
      this.results.push({
        nama: this.nama,
        a: this.a,
        b: `${this.b}%`, // Tambahkan simbol '%' untuk input B
        c,
        d,
      });
    },
    exportToPDF() {
      if (this.results.length === 0) {
        alert('Tidak ada data untuk diexport.');
        return;
      }

      const doc = new jsPDF();

      // Header
      doc.text('Persentase Jumlah', 10, 10);

      // Table Header
      const headers = [['Nama', 'A', 'B (%)', 'C', 'D']];
      const data = this.results.map(item => [item.nama, item.a, item.b, item.c, item.d]);

      // Generate Table
      autoTable(doc, {
        head: headers,
        body: data,
        startY: 20,
      });

      // Save PDF
      doc.save('Persentase_Jumlah.pdf');
    },
  },
};
</script>

<style>
.export-btn {
  background-color: #28a745;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 20px;
}

.export-btn:hover {
  background-color: #218838;
}

/* Form Styling */
form {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-bottom: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
}

input {
  padding: 10px;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
}

/* Button Styling */
button {
  background-color: #007bff;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0056b3;
}

/* Table Styling */
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

thead {
  background-color: #f2f2f2;
}

tr:nth-child(even) {
  background-color: #f9f9f9;
}

/* Responsiveness */
@media (max-width: 600px) {
  form {
    gap: 10px;
  }

  input {
    font-size: 0.9rem;
    padding: 8px;
  }

  button {
    font-size: 0.9rem;
  }

  table {
    font-size: 0.8rem;
    overflow-x: auto;
    display: block;
    white-space: nowrap;
  }
}
</style>
