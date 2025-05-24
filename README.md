// Fraktum: Протокол Вечности — Прототип сайта карточной игры
// Стартовая структура React-проекта с меню, инвентарём, открытием пака и темой тёмного фэнтези

import { useState } from 'react';
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { motion } from "framer-motion";

const exampleCards = [
  { name: "Прах Вечной Тени", rarity: "Архаичная", type: "Эффект" },
  { name: "Клятва Крови", rarity: "Легендарная", type: "Событие" },
  { name: "Зов Иллюзии", rarity: "Мифическая", type: "Тактика" },
  { name: "Тьма Надежды", rarity: "Редкая", type: "Эффект" },
  { name: "Огненный Клинок Севера", rarity: "Экзотическая", type: "Событие" }
];

export default function FraktumGame() {
  const [packOpened, setPackOpened] = useState(false);
  const [cards, setCards] = useState([]);

  const openPack = () => {
    setPackOpened(true);
    setCards(shuffle(exampleCards).slice(0, 5));
  };

  const shuffle = (arr) => arr.sort(() => Math.random() - 0.5);

  return (
    <div className="min-h-screen bg-gradient-to-br from-gray-900 to-black text-white p-6">
      <h1 className="text-4xl font-bold text-center mb-10 tracking-widest">🕯️ FRAKTUM: ПРОТОКОЛ ВЕЧНОСТИ</h1>

      <div className="flex justify-center mb-10">
        <Button onClick={openPack} className="text-xl px-6 py-3 rounded-2xl shadow-lg bg-purple-800 hover:bg-purple-900">
          Открыть пак (5 карт)
        </Button>
      </div>

      {packOpened && (
        <div className="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-5 gap-4 justify-center">
          {cards.map((card, index) => (
            <motion.div
              key={index}
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ delay: index * 0.2 }}
            >
              <Card className="bg-gradient-to-tr from-gray-800 to-gray-700 text-center border-2 border-purple-700 rounded-2xl">
                <CardContent className="p-4">
                  <h2 className="text-xl font-semibold mb-2">{card.name}</h2>
                  <p className="text-sm italic text-purple-400">{card.type}</p>
                  <p className="text-sm text-yellow-500 mt-1">{card.rarity}</p>
                </CardContent>
              </Card>
            </motion.div>
          ))}
        </div>
      )}
    </div>
  );
}
