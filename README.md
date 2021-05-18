# libretrodb

A small tool to read [retroarch databases](https://github.com/libretro/libretro-database).

Download the [rdb](https://github.com/libretro/libretro-database/tree/master/rdb) files and read them using this library.

This JS / TS library is a port from [libretro-db](https://github.com/libretro/RetroArch/tree/master/libretro-db) based on the [rarchdb](https://git.m4xw.net/Switch/RetroArch/RetroArch/-/tree/0d5d19f72e1496666900901f6ab8041bfaf74f04/rarchdb) code.

## Installation

```bash
npm install --save libretrodb
```
or
```bash
yarn add libretrodb
```

## Usage

```typescript
import { Libretrodb } from 'libretrodb';
const db = await Libretrodb.from('file.rdb');

// get all database entries
const entries = db.getEntries();

// or seeach for a hash (crc, md5 or sha1)
const entry = db.searchHash('f25b77795db4204d282453184aa6c8363bd07c42');
console.log(entry);
```
```bash
{
  name: '007 Multispy (ZX-Guaranteed)',
  description: '007 Multispy (ZX-Guaranteed)',
  rom_name: '007 Multispy (1987)(ZX-Guaranteed).opd',
  size: 184320,
  crc: '017fa7e9',
  md5: '4c8249a291081522702f81e80f6dd333',
  sha1: 'f25b77795db4204d282453184aa6c8363bd07c42'
}
```

## API

### Libretrodb.from(path: string, options?: Options)

Load a database file.

- path `string` path of the database file
- options `object`
    - bufferToString `boolean` Convert binary buffers to hex strings (optional, default `true`)
    - indexHashes `boolean` Index `crc`, `md5` and `sha1` in order to search them using `searchHash` (optional, default `true`)
    
### getEntries()

Returns the entries read.

### searchHash(hex: string)

Returns the entry matching with the hash (as hex string).

### Entry Results

The entries are records without any property short list. The TypeScript `Entry` definition is based on a full scan of the whole [rdb file list](https://github.com/libretro/libretro-database/tree/master/rdb).

```typescript
export type Entry<BinType extends Buffer |string> = {
  name?: string;
  description?: string;
  rom_name?: string;
  size?: number;
  crc?: BinType;
  md5?: BinType;
  sha1?: BinType;
  serial?: BinType;
  genre?: string;
  franchise?: string;
  releasemonth?: number;
  releaseyear?: number;
  developer?: string;
  publisher?: string;
  users?: number;
  edge_rating?: number;
  edge_issue?: number;
  esrb_rating?: string;
  origin?: string;
  rumble?: number;
  edge_review?: string;
  famitsu_rating?: number;
  enhancement_hw?: string;
  elspa_rating?: string;
  analog?: number;
}
```

## License

This project is licensed under the MIT License.