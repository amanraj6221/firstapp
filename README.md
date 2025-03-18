import React, { useEffect, useState } from 'react';

const ProductDetails = () => {
 
  const [product, setProduct] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  
  useEffect(() => {
    fetch('https://fakestoreapi.com/products/1')
      .then((res) => res.json())  
      .then((json) => {
        setProduct(json);  
        setLoading(false);  
      })
      .catch((err) => {
        setError(err);  
        setLoading(false);
      });
  }, []); 

  if (loading) {
    return <div>Loading...</div>;  
  }

  if (error) {
    return <div>Error: {error.message}</div>;  
  }

  return (
    <div className="card" style={{ width: '18rem' }}>
      <img src={product.image} className="card-img-top" alt={product.title} />
      <div className="card-body">
        <h5 className="card-title">{product.title}</h5>
        <p className="card-text">{product.description}</p>
        <p className="card-text">Price: ${product.price}</p>
        <p className="card-text">Category: {product.category}</p>
        <p className="card-text">Rating: {product.rating.rate} (Rated {product.rating.count} times)</p>
      </div>
    </div>
  );
};

export default ProductDetails;
