# Translator
A web about translator
import React, { useState } from 'react';
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card';
import { Select } from '@/components/ui/select';
import { Button } from '@/components/ui/button';
import { Upload } from 'lucide-react';

const PdfLanguageConverter = () => {
  const [selectedFile, setSelectedFile] = useState(null);
  const [targetLanguage, setTargetLanguage] = useState('en');
  const [isConverting, setIsConverting] = useState(false);

  const languages = [
    { value: 'en', label: 'Inggris' },
    { value: 'id', label: 'Indonesia' },
    { value: 'ja', label: 'Jepang' },
    { value: 'ko', label: 'Korea' },
    { value: 'zh', label: 'Mandarin' },
    { value: 'ar', label: 'Arab' },
    { value: 'es', label: 'Spanyol' },
    { value: 'fr', label: 'Prancis' },
    { value: 'de', label: 'Jerman' }
  ];

  const handleFileChange = (event) => {
    const file = event.target.files[0];
    if (file && file.type === 'application/pdf') {
      setSelectedFile(file);
    } else {
      alert('Mohon upload file PDF');
    }
  };

  const handleLanguageChange = (event) => {
    setTargetLanguage(event.target.value);
  };

  const handleConvert = () => {
    if (!selectedFile) {
      alert('Silakan pilih file PDF terlebih dahulu');
      return;
    }
    setIsConverting(true);
    // Simulasi proses konversi
    setTimeout(() => {
      setIsConverting(false);
      alert('Konversi selesai! File akan otomatis terunduh.');
    }, 2000);
  };

  return (
    <Card className="w-full max-w-lg mx-auto">
      <CardHeader>
        <CardTitle className="text-2xl font-bold text-center">Konverter Bahasa PDF</CardTitle>
      </CardHeader>
      <CardContent className="space-y-6">
        <div className="space-y-4">
          <label className="block text-sm font-medium">Upload PDF</label>
          <div className="flex items-center justify-center w-full">
            <label className="flex flex-col items-center justify-center w-full h-32 border-2 border-dashed rounded-lg cursor-pointer bg-gray-50 hover:bg-gray-100">
              <div className="flex flex-col items-center justify-center pt-5 pb-6">
                <Upload className="w-10 h-10 mb-3 text-gray-400" />
                <p className="mb-2 text-sm text-gray-500">
                  <span className="font-semibold">Klik untuk upload</span> atau drag & drop
                </p>
                <p className="text-xs text-gray-500">PDF (MAX. 10MB)</p>
              </div>
              <input
                type="file"
                className="hidden"
                accept=".pdf"
                onChange={handleFileChange}
              />
            </label>
          </div>
          {selectedFile && (
            <p className="text-sm text-gray-500">
              File terpilih: {selectedFile.name}
            </p>
          )}
        </div>

        <div className="space-y-4">
          <label className="block text-sm font-medium">Pilih Bahasa Tujuan</label>
          <select
            className="w-full p-2 border rounded-md"
            value={targetLanguage}
            onChange={handleLanguageChange}
          >
            {languages.map((lang) => (
              <option key={lang.value} value={lang.value}>
                {lang.label}
              </option>
            ))}
          </select>
        </div>

        <Button
          className="w-full"
          onClick={handleConvert}
          disabled={!selectedFile || isConverting}
        >
          {isConverting ? 'Sedang Mengkonversi...' : 'Konversi PDF'}
        </Button>
      </CardContent>
    </Card>
  );
};

export default PdfLanguageConverter;
