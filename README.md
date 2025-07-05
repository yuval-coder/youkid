{
  "id": "org.youkid.talents",
  "version": "1.0.0",
  "name": "YouKid כוכבים",
  "description": "תוסף סטרימיו לצפייה בכוכבי הילדים של YouKid",
  "resources": ["catalog", "meta"],
  "types": ["movie"],
  "catalogs": [
    {
      "type": "movie",
      "id": "youkid_talents",
      "name": "YouKid Talents"
    }
  ]
}
const { addonBuilder } = require("stremio-addon-sdk");

const metas = [
  {
    id: "yuval",
    type: "movie",
    name: "יובל המבולבל",
    poster: "https://www.youkid.co.il/talents/yuval/poster.jpg",
    description: "כוכב הילדים יובל המבולבל"
  },
  {
    id: "riko",
    type: "movie",
    name: "ריקו",
    poster: "https://www.youkid.co.il/talents/riko/poster.jpg",
    description: "כוכב הילדים ריקו"
  },
  {
    id: "miki",
    type: "movie",
    name: "מיקי",
    poster: "https://www.youkid.co.il/talents/miki/poster.jpg",
    description: "מיקי"
  }
];

const builder = new addonBuilder({
  id: "org.youkid.talents",
  version: "1.0.0",
  name: "YouKid כוכבים",
  description: "תוסף סטרימיו לצפייה בכוכבי הילדים של YouKid",
  types: ["movie"],
  catalogs: [
    {
      type: "movie",
      id: "youkid_talents"
    }
  ],
  resources: ["catalog", "meta"]
});

builder.defineCatalogHandler(() => {
  return Promise.resolve({ metas });
});

builder.defineMetaHandler(({ id }) => {
  const meta = metas.find(m => m.id === id);
  return Promise.resolve({ meta });
});

module.exports = builder.getInterface();
const express = require("express");
const addonInterface = require("./addon");

const app = express();

app.get("/manifest.json", (req, res) => {
  res.sendFile(__dirname + "/manifest.json");
});

app.use("/", addonInterface);

app.listen(7000, () => {
  console.log("YouKid Addon running on http://localhost:7000");
});
