import React, { useState, useEffect } from 'react';
import { Button } from '@/components/ui/button';
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card';

const vegetables = [
  { name: 'طماطم', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/8/88/Bright_red_tomato_and_cross_section02.jpg/320px-Bright_red_tomato_and_cross_section02.jpg' },
  { name: 'خيار', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/9/96/ARS_cucumber.jpg/320px-ARS_cucumber.jpg' },
  { name: 'جزر', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Vegetable-Carrot-Bundle-wStalks.jpg/320px-Vegetable-Carrot-Bundle-wStalks.jpg' },
  { name: 'بصل', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/2/25/Onion_on_White.JPG/320px-Onion_on_White.JPG' },
  { name: 'فلفل', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/7/74/Green_Bell_Peppers_2.jpg/320px-Green_Bell_Peppers_2.jpg' },
  { name: 'باذنجان', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/7/76/Solanum_melongena_24_08_2012_%281%29.JPG/320px-Solanum_melongena_24_08_2012_%281%29.JPG' },
  { name: 'بطاطس', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/ab/Patates.jpg/320px-Patates.jpg' },
  { name: 'كوسة', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/9/92/Courgette_jaune_et_verte.jpg/320px-Courgette_jaune_et_verte.jpg' },
  { name: 'ثوم', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Garlic_bulbs.jpg/320px-Garlic_bulbs.jpg' },
  { name: 'خس', image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Iceberg_lettuce_in_SB.jpg/320px-Iceberg_lettuce_in_SB.jpg' },
];

const ArabicVegetablesGame = () => {
  const [currentVegetable, setCurrentVegetable] = useState(null);
  const [options, setOptions] = useState([]);
  const [score, setScore] = useState(0);

  const getRandomVegetables = (count) => {
    const shuffled = [...vegetables].sort(() => 0.5 - Math.random());
    return shuffled.slice(0, count);
  };

  const startNewRound = () => {
    const [correct, ...wrongOnes] = getRandomVegetables(3);
    setCurrentVegetable(correct);
    setOptions([correct, ...wrongOnes].sort(() => 0.5 - Math.random()));
  };

  useEffect(() => {
    startNewRound();
  }, []);

  const handleAnswer = (vegetable) => {
    if (vegetable.name === currentVegetable.name) {
      setScore(score + 1);
    }
    startNewRound();
  };

  return (
    <Card className="w-96 mx-auto">
      <CardHeader>
        <CardTitle className="text-center">تعلم الخضروات باللغة العربية</CardTitle>
      </CardHeader>
      <CardContent>
        {currentVegetable && (
          <div className="flex flex-col items-center">
            <img src={currentVegetable.image} alt="Vegetable" className="w-32 h-32 object-cover mb-4 rounded-lg" />
            <div className="grid grid-cols-1 gap-2 w-full">
              {options.map((option) => (
                <Button
                  key={option.name}
                  onClick={() => handleAnswer(option)}
                  className="w-full"
                >
                  {option.name}
                </Button>
              ))}
            </div>
            <p className="mt-4">النتيجة: {score}</p>
          </div>
        )}
      </CardContent>
    </Card>
  );
};

export default ArabicVegetablesGame;
