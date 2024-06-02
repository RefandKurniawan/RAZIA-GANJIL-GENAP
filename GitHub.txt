function kenaRazia(date, data) {
  // Daftar rute ganjil genap
  const ganjilGenapRoutes = ["Gajah Mada", "Hayam Wuruk", "Sisingamangaraja", "Panglima Polim", "Fatmawati", "Tomang Raya"];
  
  // Menentukan apakah tanggal adalah ganjil atau genap
  const isDateGanjil = date % 2 !== 0;
  
  let results = [];

  for (let i = 0; i < data.length; i++) {
    const vehicle = data[i];
    
    // Hanya memeriksa kendaraan tipe "Mobil"
    if (vehicle.type === "Mobil") {
      // Mengambil digit terakhir dari nomor plat
      const platNumber = vehicle.plat.split(' ')[1];
      const lastDigit = parseInt(platNumber[platNumber.length - 1]);
      const isPlatGanjil = lastDigit % 2 !== 0;
      
      let tilangCount = 0;

      for (let j = 0; j < vehicle.rute.length; j++) {
        const route = vehicle.rute[j];
        
        // Memeriksa apakah rute termasuk rute ganjil genap
        for (let k = 0; k < ganjilGenapRoutes.length; k++) {
          if (route === ganjilGenapRoutes[k]) {
            if ((isDateGanjil && !isPlatGanjil) || (!isDateGanjil && isPlatGanjil)) {
              tilangCount++;
            }
          }
        }
      }

      if (tilangCount > 0) {
        results.push({ name: vehicle.name, tilang: tilangCount });
      }
    }
  }

  return results;
}

console.log(
  kenaRazia(27, [
    {
      name: "Denver",
      plat: "B 2791 KDS",
      type: "Mobil",
      rute: ["TB Simatupang", "Panglima Polim", "Depok", "Senen Raya"]
    },
    {
      name: "Toni",
      plat: "B 1212 JBB",
      type: "Mobil",
      rute: [
        "Pintu Besar Selatan",
        "Panglima Polim",
        "Depok",
        "Senen Raya",
        "Kemang"
      ]
    },
    {
      name: "Stark",
      plat: "B 444 XSX",
      type: "Motor",
      rute: ["Pondok Indah", "Depok", "Senen Raya", "Kemang"]
    },
    {
      name: "Anna",
      plat: "B 678 DD",
      type: "Mobil",
      rute: [
        "Fatmawati",
        "Panglima Polim",
        "Depok",
        "Senen Raya",
        "Kemang",
        "Gajah Mada"
      ]
    }
  ])
);

// Output yang diharapkan: [ { name: 'Toni', tilang: 1 }, { name: 'Anna', tilang: 3 } ]
