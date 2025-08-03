my-love-site/
├─ public/
│   ├─ rabia1.jpg
│   ├─ rabia2.jpg
│   └─ romantic-music.mp3
├─ pages/
│   └─ index.js
├─ package.json
import { useEffect, useState } from "react";
import { motion, AnimatePresence } from "framer-motion";

const photos = [
  "/rabia1.jpg",
  "/rabia2.jpg"
];

export default function Home() {
  const [currentPhoto, setCurrentPhoto] = useState(0);
  const [audio] = useState(typeof Audio !== "undefined" ? new Audio("/romantic-music.mp3") : null);

  useEffect(() => {
    const interval = setInterval(() => {
      setCurrentPhoto((prev) => (prev + 1) % photos.length);
    }, 4000);
    return () => clearInterval(interval);
  }, []);

  useEffect(() => {
    if (audio) {
      audio.loop = true;
      audio.volume = 0.3;
      audio.play().catch(() => {});
    }
    return () => {
      if (audio) audio.pause();
    };
  }, [audio]);

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-100 to-pink-200 flex flex-col items-center justify-center p-4 text-center">
      <AnimatePresence mode="wait">
        <motion.img
          key={currentPhoto}
          src={photos[currentPhoto]}
          alt="Bizim Fotoğraf"
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          exit={{ opacity: 0 }}
          transition={{ duration: 1 }}
          className="rounded-2xl shadow-lg w-full max-w-md mb-6"
        />
      </AnimatePresence>

      <div className="bg-white/70 rounded-2xl shadow-xl max-w-xl p-6">
        <p className="text-xl font-semibold mb-2 text-rose-600">
          Sana olan sevgim, kelimelere sığmayacak kadar gerçek.
        </p>
        <p className="text-lg text-gray-800">
          Yanımda olduğun her an, hayat daha güzel.
        </p>
        <p className="text-sm text-gray-600 mt-4">Beraber: 4 ay 22 gün (144 gün)</p>
      </div>

      <div className="mt-10 text-xs text-gray-500">
        Her Şey Seninle Güzel çalıyor... 🎵
      </div>
    </div>
  );
}
