### NFT commitment length limit

NFT commitments can store up to 40 bytes of data as local state. If more data is needed, you can hash the full state and store only the hash in the commitment data. Later, when required, the full state must be provided and validated against the stored hash.