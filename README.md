public/
  sound/
    background.mp3
    love-unlock.mp3
    kelaskan.mp3
  images/
    key.png
    heart-lock.png
pages/
  index.jsimport { useState, useEffect } from 'react';
import { motion } from 'framer-motion';

export default function Home() {
  const [unlocked, setUnlocked] = useState(false);
  const [denied, setDenied] = useState(false);

  useEffect(() => {
    const bg = new Audio('/sound/background.mp3');
    bg.loop = true;
    bg.volume = 0.3;
    bg.play();
  }, []);

  const handleYes = () => {
    new Audio('/sound/love-unlock.mp3').play();
    setUnlocked(true);
  };

  const handleNo = () => {
    new Audio('/sound/kelaskan.mp3').play();
    setDenied(true);
  };

  return (
    <main className="min-h-screen bg-gradient-to-br from-pink-100 via-yellow-100 to-white flex flex-col items-center justify-center p-6">
      <motion.h1 className="text-5xl font-bold text-pink-700 mb-4" initial={{ y:-50, opacity:0 }} animate={{ y:0, opacity:1 }} transition={{ duration:1 }}>
        Hai TeTeh Yuli 🌸
      </motion.h1>
      <motion.p className="text-center text-gray-700 mb-6 max-w-xl"
        initial={{ opacity:0 }} animate={{ opacity:1 }} transition={{ delay:1, duration:1 }}>
        Si adek SMK ini pengen banget bilang: “Aku suka sama teteh…” 😉
      </motion.p>

      {!unlocked && !denied && (
        <motion.div className="flex gap-8"
          initial={{ opacity:0 }} animate={{ opacity:1 }} transition={{ delay:2 }}>
          <button onClick={handleYes} className="px-6 py-3 bg-pink-500 hover:bg-pink-600 text-white rounded-full">Iya 💖</button>
          <button onClick={handleNo} className="px-6 py-3 bg-gray-300 hover:bg-gray-400 text-gray-700 rounded-full">Tidak 😢</button>
        </motion.div>
      )}

      {unlocked && (
        <motion.div className="mt-8 text-center"
          initial={{ opacity:0 }} animate={{ opacity:1 }} transition={{ delay:0.5 }}>
          <img src="/images/heart-lock.png" alt="Love Unlocked" className="mx-auto w-40" />
          <motion.p className="mt-4 text-pink-600 text-xl font-semibold"
            initial={{ scale:0.8, opacity:0 }} animate={{ scale:1, opacity:1 }} transition={{ delay:1 }}>
            *Love unlocked!*<br/>
            Sekarang bilang sayangnya beneran ya 😆😖
          </motion.p>
        </motion.div>
      )}

      {denied && (
        <motion.div className="mt-8 text-center"
          initial={{ opacity:0 }} animate={{ opacity:1 }} transition={{ delay:0.5 }}>
          <img src="/images/key.png" alt="Key" className="mx-auto w-32" />
          <motion.p className="mt-4 text-gray-600 text-lg"
            initial={{ opacity:0 }} animate={{ opacity:1 }} transition={{ delay:1 }}>
            Gak apa-apa, TeTeh…  
            Saya ikhlas kok 😌
          </motion.p>
        </motion.div>
      )}
    </main>
);
}
